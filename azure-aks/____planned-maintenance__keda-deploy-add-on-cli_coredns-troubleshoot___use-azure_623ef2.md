---
merged_at: 2026-01-28T07:16:09.863766
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/planned-maintenance -->

# Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use planned maintenance to schedule and control cluster and node image upgrades in Azure Kubernetes Service (AKS).

Regular maintenance is performed on your AKS cluster automatically. There are two types of maintenance operations:

**AKS-initiated maintenance**involves the weekly releases that AKS performs to keep your cluster up to date with the latest features and fixes.**User-initiated maintenance**includes[cluster auto-upgrades](upgrade-cluster)and[node operating system (OS) automatic security updates](auto-upgrade-node-image).

When you use the feature of planned maintenance in AKS, you can run both types of maintenance in a cadence of your choice to minimize workload impact.

Note

You can use planned maintenance to schedule the timing of automatic upgrades, but enabling or disabling planned maintenance doesn't enable or disable automatic upgrades.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, see
[Create an AKS cluster](learn/quick-kubernetes-deploy-cli). - If you're using the Azure CLI, upgrade to the latest version using the
command.`az upgrade`


## Considerations

When you use planned maintenance, the following considerations apply:

- AKS reserves the right to break planned maintenance windows for unplanned, reactive maintenance operations that are urgent or critical. These maintenance operations might even run during the
`notAllowedTime`

or`notAllowedDates`

periods defined in your configuration. - Maintenance operations are considered
*best effort only*and aren't guaranteed to occur within a specified window.

## Schedule configuration types for planned maintenance

Three schedule configuration types are available for planned maintenance:

`default`

is a basic configuration for controlling AKS releases, which covers control plane components and system add-ons upgrade. The releases can take up to two weeks to roll out to all regions from the initial time of shipping, because of Azure safe deployment practices.Choose

`default`

to schedule these updates in a manner that's least disruptive for you. You can monitor the status of an ongoing AKS release by region with the[weekly release tracker](release-tracker).`aksManagedAutoUpgradeSchedule`

controls when to perform cluster upgrades scheduled by your designated auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on cluster auto-upgrade, see[Automatically upgrade an Azure Kubernetes Service cluster](upgrade-cluster).`aksManagedNodeOSUpgradeSchedule`

controls when to perform the node OS security patching scheduled by your node OS auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on node OS auto-upgrade channels, see[Automatically patch and update AKS cluster node images](auto-upgrade-node-image).

We recommend using `aksManagedAutoUpgradeSchedule`

for all cluster Kubernetes version upgrade scenarios and `aksManagedNodeOSUpgradeSchedule`

for all node OS security patching scenarios.

The `default`

option is meant exclusively for AKS weekly releases. Use `default`

if you want to control the upgrade schedule for AKS control plane components (such as API Server, ETCD, etc.) and add-ons (such as CoreDNS, Metrics Server, etc.).

All three types of configurations can coexist.

## Create a maintenance window

Note

When you're using auto-upgrade, to ensure proper functionality, use a maintenance window with a duration of four hours or more.

Note

From the 2023-05-01 API version onwards, use the properties in the following table for `default`

configuration.

An `aksManagedAutoUpgradeSchedule`

or `aksManagedNodeOSUpgradeSchedule`

maintenance window and `default`

configuration from 2023-05-01 API version onwards has the following properties:

| Name | Description | Default value |
|---|---|---|
`utcOffset` |
The time zone for cluster maintenance. | `+00:00` |
`startDate` |
The date on which the maintenance window begins to take effect. | The current date at creation time |
`startTime` |
The time for maintenance to begin, based on the time zone determined by `utcOffset` . |
Not applicable |
`schedule` |
The upgrade frequency. Three types are available: `Weekly` , `AbsoluteMonthly` , and `RelativeMonthly` . |
Not applicable |
`intervalDays` |
The interval in days for maintenance runs. It's applicable only to `aksManagedNodeOSUpgradeSchedule` . |
Not applicable |
`intervalWeeks` |
The interval in weeks for maintenance runs. | Not applicable |
`intervalMonths` |
The interval in months for maintenance runs. | Not applicable |
`dayOfWeek` |
The specified day of the week for maintenance to begin. | Not applicable |
`durationHours` |
The duration of the window for maintenance to run. | Not applicable |
`notAllowedDates` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. It's applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Deprecated properties

Note

If you create a `default`

configuration with the following deprecated properties, it migrates automatically to the new properties shown in the previous table.

**[Deprecated]** A `default`

maintenance window has the following legacy properties:

| Name | Description | Default value |
|---|---|---|
`timeInWeek` |
In a `default` configuration, this property contains the `day` and `hourSlots` values that define a maintenance window. |
Not applicable |
`timeInWeek.day` |
The day of the week to perform maintenance in a `default` configuration. |
Not applicable |
`timeInWeek.hourSlots` |
A list of hour-long time slots to perform maintenance on a particular day in a `default` configuration. |
Not applicable |
`notAllowedTime` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. This property is applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Schedule types

Four schedule types are supported: `Daily`

, `Weekly`

, `AbsoluteMonthly`

, and `RelativeMonthly`

.

The following table shows which types are available for each maintenance-configuration option:

| Schedule type | `default` |
`aksManagedClusterAutoUpgradeSchedule` |
`aksManagedNodeOSUpgradeSchedule` |
|---|---|---|---|
| Daily | Unsupported ❌ | Supported ✅ (after Jun 2025) | Supported ✅ |
| Weekly | Supported ✅ | Supported ✅ | Supported ✅ |
| AbsoluteMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |
| RelativeMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |

All of the fields shown for each schedule type are required.

A `Daily`

schedule might look like "every three days":

```
"schedule": {
"daily": {
"intervalDays": 3
}
}
```


A `Weekly`

schedule might look like "every two weeks on Friday":

```
"schedule": {
"weekly": {
"intervalWeeks": 2,
"dayOfWeek": "Friday"
}
}
```


An `AbsoluteMonthly`

schedule might look like "every three months on the first day of the month":

```
"schedule": {
"absoluteMonthly": {
"intervalMonths": 3,
"dayOfMonth": 1
}
}
```


A `RelativeMonthly`

schedule might look like "every two months on the last Monday":

```
"schedule": {
"relativeMonthly": {
"intervalMonths": 2,
"dayOfWeek": "Monday",
"weekIndex": "Last"
}
}
```


Valid values for `weekIndex`

include `First`

, `Second`

, `Third`

, `Fourth`

, and `Last`

.

## Add a maintenance window configuration

Add a maintenance window configuration to an AKS cluster using the [ az aks maintenanceconfiguration add](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-add) command.

The first example adds a new `default`

configuration that schedules maintenance to run from 1:00 AM to 5:00 AM every Monday in the `UTC`

time zone. The second example adds a new `aksManagedAutoUpgradeSchedule`

configuration that schedules maintenance to run every third Friday between 12:00 AM and 8:00 AM in the `UTC+5:30`

time zone.

```
# Add a new default configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Monday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 01:00
# Add a new aksManagedAutoUpgradeSchedule configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule --schedule-type Weekly --day-of-week Friday --interval-weeks 3 --duration 8 --utc-offset +05:30 --start-time 00:00
```


## Update an existing maintenance window

Update an existing maintenance configuration using the [ az aks maintenanceconfiguration update](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-update) command.

The following example updates the `default`

configuration to schedule maintenance to run from 2:00 AM to 6:00 AM every Friday:

```
az aks maintenanceconfiguration update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Friday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 02:00
```


## List all maintenance windows in an existing cluster

List the current maintenance configuration windows in your AKS cluster using the [ az aks maintenanceconfiguration list](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-list) command:

```
az aks maintenanceconfiguration list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Show a specific maintenance configuration window in an existing cluster

View a specific maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration show](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-show) command with the

`--name`

parameter:```
az aks maintenanceconfiguration show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule
```


The following example output shows the maintenance window for `aksManagedAutoUpgradeSchedule`

:

```
{
"id": "/subscriptions/<subscription>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/maintenanceConfigurations/aksManagedAutoUpgradeSchedule",
"maintenanceWindow": {
"durationHours": 4,
"notAllowedDates": [
{
"end": "2024-01-05",
"start": "2023-12-23"
}
],
"schedule": {
"absoluteMonthly": {
"dayOfMonth": 1,
"intervalMonths": 3
},
"daily": null,
"relativeMonthly": null,
"weekly": null
},
"startDate": "2023-01-20",
"startTime": "09:00",
"utcOffset": "-08:00"
},
"name": "aksManagedAutoUpgradeSchedule",
"notAllowedTime": null,
"resourceGroup": "myResourceGroup",
"systemData": null,
"timeInWeek": null,
"type": null
}
```


## Delete a maintenance configuration window in an existing cluster

Delete a maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration delete](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-delete) command.

The following example deletes the `autoUpgradeSchedule`

maintenance configuration:

```
az aks maintenanceconfiguration delete --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name autoUpgradeSchedule
```


## Frequently asked questions (FAQ)

### How can I check the existing maintenance configurations in my cluster?

Use the `az aks maintenanceconfiguration show`

command.

### Can reactive, unplanned maintenance happen during the `notAllowedDates`

periods too?

Yes. AKS reserves the right to break these windows for unplanned, reactive maintenance operations that are urgent or critical.

### How can I tell if a maintenance event occurred?

For releases, check your cluster's region and look up information in [weekly releases](release-tracker) to see if it matches your maintenance schedule. To view the status of your automatic upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events, as mentioned in [Upgrade an AKS cluster](upgrade-cluster).

AKS also emits upgrade-related Azure Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I use more than one maintenance configuration at the same time?

Yes, you can run all three configurations simultaneously: `default`

, `aksManagedAutoUpgradeSchedule`

, and `aksManagedNodeOSUpgradeSchedule`

. If the windows overlap, AKS decides the running order.

### I configured a maintenance window, but the upgrade didn't happen. Why?

AKS auto-upgrade needs a certain amount of time, usually not more than 15 minutes, to take the maintenance window into consideration. We recommend at least 15 minutes between the creation or update of a maintenance configuration and the scheduled start time.

Also, ensure that your cluster is started when the planned maintenance window starts. If the cluster is stopped, its control plane is deallocated and no operations can be performed.

### Why was one of my agent pools upgraded outside the maintenance window?

If an agent pool isn't upgraded (for example, because pod disruption budgets prevented it), it might be upgraded later, outside the maintenance window. This scenario is referred to as a *catch-up upgrade*. It avoids letting agent pools be upgraded with a different version from the AKS control plane.

Another reason why an agent pool could be upgraded unexpectedly is when there's no defined maintenance configuration or if it was deleted. In that case, a cluster with auto-upgrade *but without a maintenance configuration* is upgraded at random times (*fallback schedule*), which might be an undesired timeframe.

### Are there any best practices for the maintenance configurations?

We recommend setting the [node OS security updates](auto-upgrade-node-image) schedule to a weekly cadence if you're using the `NodeImage`

channel, because a new node image is shipped every week. You can also opt in for the `SecurityPatch`

channel to receive daily security updates.

You can set the [auto-upgrade](auto-upgrade-cluster) schedule to a monthly cadence to stay current with the Kubernetes N-2 [support policy](support-policies).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

### Can I configure all my clusters in a single subscription to use the same maintenance configuration?

We don't recommend using the same maintenance configuration for multiple clusters in a single subscription, as doing so can lead to ARM throttling errors causing cluster upgrades to fail. Instead, we recommend staggering the maintenance windows for each cluster to avoid these errors.

### Why did my node pools get upgraded twice during the same maintenance window?

If a newer version of the node image becomes available during the maintenance window, AKS performs a second upgrade to ensure that your node pools are running the latest version. This behavior is normal and doesn't indicate an issue.

## Related content

To get started with upgrading your AKS cluster, see [Upgrade options for AKS clusters](upgrade-cluster).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-cli -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using the Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to install the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using the Azure CLI.

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Install the KEDA add-on with Azure CLI

To install the KEDA add-on, use `--enable-keda`

when creating or updating a cluster.

## Enable the KEDA add-on on your AKS cluster

Note

While KEDA provides various customization options, the KEDA add-on currently provides basic common configuration.

If you require custom configurations, you can manually edit the KEDA YAML files to customize the installation. **Azure doesn't offer support for custom configurations**.

### Create a new AKS cluster with KEDA add-on enabled

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create a new AKS cluster using the

command and enable the KEDA add-on using the`az aks create`

`--enable-keda`

flag.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda \ --generate-ssh-keys`


### Enable the KEDA add-on on an existing AKS cluster

Update an existing cluster using the

command and enable the KEDA add-on using the`az aks update`

`--enable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Verify the KEDA add-on is installed on your cluster

Verify the KEDA add-on is installed on your cluster using the

command and set the`az aks show`

`--query`

parameter to`workloadAutoScalerProfile.keda.enabled`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query "workloadAutoScalerProfile.keda.enabled"`

The following example output shows the KEDA add-on is installed on the cluster:

`true`


## Verify KEDA is running on your cluster

Verify the KEDA add-on is running on your cluster using the

`kubectl get pods`

command.`kubectl get pods -n kube-system`

The following example output shows the KEDA operator, admissions hook, and metrics API server are installed on the cluster:

`keda-admission-webhooks-**********-2n9zl 1/1 Running 0 3d18h keda-admission-webhooks-**********-69dkg 1/1 Running 0 3d18h keda-operator-*********-4hb5n 1/1 Running 0 3d18h keda-operator-*********-pckpx 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-gqg4s 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-trfcb 1/1 Running 0 3d18h`


## Verify the KEDA version on your cluster

To verify the version of your KEDA, use `kubectl get crd/scaledobjects.keda.sh -o yaml `

. For example:

```
kubectl get crd/scaledobjects.keda.sh -o yaml
```


The following example output shows the configuration of KEDA in the `app.kubernetes.io/version`

label:

```
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
annotations:
controller-gen.kubebuilder.io/version: v0.9.0
meta.helm.sh/release-name: aks-managed-keda
meta.helm.sh/release-namespace: kube-system
creationTimestamp: "2023-08-09T15:58:56Z"
generation: 1
labels:
app.kubernetes.io/component: operator
app.kubernetes.io/managed-by: Helm
app.kubernetes.io/name: keda-operator
app.kubernetes.io/part-of: keda-operator
app.kubernetes.io/version: 2.10.1
helm.toolkit.fluxcd.io/name: keda-adapter-helmrelease
helm.toolkit.fluxcd.io/namespace: 64d3b6fd3365790001260647
name: scaledobjects.keda.sh
resourceVersion: "1421"
uid: 29109c8c-638a-4bf5-ac1b-c28ad9aa11fa
spec:
conversion:
strategy: None
group: keda.sh
names:
kind: ScaledObject
listKind: ScaledObjectList
plural: scaledobjects
shortNames:
- so
singular: scaledobject
scope: Namespaced
# Redacted due to length
```


## Disable the KEDA add-on on your AKS cluster

Disable the KEDA add-on on your cluster using the

command with the`az aks update`

`--disable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-keda`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster using the Azure CLI.

With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/coredns-troubleshoot -->

# Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides troubleshooting guidance for various CoreDNS issues on Azure Kubernetes Service (AKS).

## Debug DNS resolution issues

For general CoreDNS troubleshooting steps, such as checking the endpoints or resolution, see [Debugging DNS resolution](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/).

## Troubleshoot CoreDNS pod traffic imbalance

You might see one or two CoreDNS pods showing significantly higher CPU usage and handling more DNS queries than others, even with multiple CoreDNS pods running in your AKS cluster. This is a [known issue](https://github.com/kubernetes/kubernetes/issues/76517#issuecomment-490731578) in Kubernetes and can lead to one of the CoreDNS pods being overloaded and crashing.

This uneven distribution of DNS queries is primarily caused by User Datagram Protocol (UDP) load balancing limitations in Kubernetes. The platform uses a five-tuple hash (source IP, source port, destination IP, destination port, protocol) to distribute UDP traffic, so if an application reuses the same source port for DNS queries, all queries from that client are routed to the same CoreDNS pod. This distribution method can result in a single pod handling a disproportionate amount of traffic. Additionally, some applications use connection pooling and reuse DNS connections. This behavior can further concentrate DNS queries on a single CoreDNS pod, increasing the imbalance and the risk of overloading and potential crashes.

The following sections help you troubleshoot and mitigate this issue.

### Enable DNS query logging

Enable DNS query logging to capture required DNS query logs from CoreDNS pods.

Add the following configuration to your

`coredns-custom`

ConfigMap:`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: log.override: | # You can select any name here, but it must end with the .override file extension log`

Apply the ConfigMap changes using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`

View the CoreDNS debug logging using the

`kubectl logs`

command.`kubectl logs --namespace kube-system -l k8s-app=kube-dns`


### Check your CoreDNS pod traffic distribution

Get the names of all CoreDNS pods in your cluster using the

command.`kubectl get pods`

`kubectl get pods --namespace kube-system -l k8s-app=kube-dns`

Review the logs for each CoreDNS pod to analyze DNS query patterns using the

command. Repeat this command for all CoreDNS pods, replacing`kubectl logs`

`<coredns-pod-x>`

with the actual pod names.`kubectl logs --namespace kube-system <coredns-pod-x>`

In the outputs, look for repeated client IP addresses and ports that appear only in the logs of a single CoreDNS pod. This indicates that DNS queries from certain clients aren't being distributed evenly.

Example log output:

`[INFO] 10.244.0.247:5556 - 42621 "A IN myservice.default.svc.cluster.local. udp 28" NOERROR qr,aa,rd 106 0.000141s`

In this example log entry:

`10.244.0.247`

is the client IP address making the DNS query.`5556`

is the client source port.`42621`

is the query ID.

**If you see the same client IP and port repeatedly in only one pod's logs, this confirms a traffic imbalance**.

### Mitigate CoreDNS pod traffic imbalance

If you notice an imbalance, your application could be reusing UDP source ports or pooling their connections. Based on the root cause, you can take the following mitigation actions:

**Caused by UDP source port reuse**: UDP source port reuse occurs when a client application sends multiple DNS queries from the same UDP source port. If this is the issue, update your applications or DNS clients to randomize source ports for each DNS query, which helps distribute requests more evenly across pods.**Caused by connection pooling**: Connection pools are mechanisms applications use to reuse existing network connections instead of creating a new connection for each request. While this improves efficiency, it can result in all DNS queries from an application being sent over the same connection, and thus routed to the same CoreDNS pod. To mitigate this, adjust your application's DNS connection handling by reducing connection Time to Live (TTL) or randomizing connection creation, ensuring queries aren't concentrated on a single CoreDNS pod.

These changes can help achieve a more balanced DNS query distribution and reduce the risk of overloading individual pods.

## Troubleshoot invalid search domain completions for internal.cloudapp.net and reddog.microsoft.com

Azure DNS configures a default search domain of `<VNET_ID>.<REGION>.internal.cloudapp.net`

in virtual networks (VNets) using Azure DNS and a nonfunctional stub `reddog.microsoft.com`

in VNets using custom DNS servers. For more information, see the [Name resolution for resources documentation](/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

Kubernetes configures pod DNS settings with `ndots: 5`

to properly support cluster service hostname resolution. These two configurations combine to result in invalid search domain completion queries that never succeed being sent to upstream name servers while the system processes through the domain search list. These invalid queries cause name resolution delays and can place extra load on upstream DNS servers.

As of the *v20241025* AKS release, AKS configures CoreDNS to respond with `NXDOMAIN`

in the following cases in order to prevent these invalid search domain completion queries from being forwarded to upstream DNS:

- Any query for the root domain or a subdomain of
`reddog.microsoft.com`

. - Any query for a subdomain of
`internal.cloudapp.net`

that has seven or more labels in the domain name.- This configuration allows virtual machine (VM) resolution by hostname to still succeed. For example, CoreDNS sends
`aks12345.myvnetid.myregion.internal.cloudapp.net`

(*six*labels) to Azure DNS, but rejects`mcr.microsoft.com.myvnetid.myregion.internal.cloudapp.net`

(*eight*labels).

- This configuration allows virtual machine (VM) resolution by hostname to still succeed. For example, CoreDNS sends

This block is implemented in the default server block in the CoreFile for the cluster. If needed, you can disable this rejection configuration by creating custom server blocks for the appropriate domain with a forward plugin enabled:

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to update the IP addresses and hostnames with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom # This is the name of the ConfigMap you can overwrite with your changes namespace: kube-system data: override-block.server: | internal.cloudapp.net:53 { errors cache 30 forward . /etc/resolv.conf } reddog.microsoft.com:53 { errors cache 30 forward . /etc/resolv.conf }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Troubleshoot CoreDNS autoscaling issues

To troubleshoot CoreDNS autoscaling issues, see [Autoscaling CoreDNS in Azure Kubernetes Service (AKS)](coredns-autoscale).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-policy -->

# Secure your Azure Kubernetes Service (AKS) clusters with Azure Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can apply and enforce built-in security policies on your Azure Kubernetes Service (AKS) clusters using [Azure Policy](/en-us/azure/governance/policy/overview). Azure Policy helps enforce organizational standards and assess compliance at-scale. After you install the [Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes), you can apply individual policy definitions or groups of policy definitions called initiatives (sometimes called policysets) to your cluster. See [Azure Policy built-in definitions for AKS](policy-reference) for a complete list of AKS policy and initiative definitions.

This article shows you how to apply policy definitions to your cluster and verify those assignments are being enforced.

## Prerequisites

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the
[Azure Policy add-on for AKS installed on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks).

## Assign a built-in policy definition or initiative

You can apply a policy definition or initiative in the Azure portal using the following steps:

- Navigate to the Azure Policy service in Azure portal called
**Policy**. - In the left pane of the Azure Policy page, select
**Definitions**. - Under
**Categories**, select`Kubernetes`

. - Choose the policy definition or initiative you want to apply. For this example, select the
**Kubernetes cluster pod security baseline standards for Linux-based workloads**initiative. - Select
**Assign**. - Set the
**Scope**to the resource group of the AKS cluster with the Azure Policy add-on enabled. - Select the
**Parameters**page and update the**Effect**from`audit`

to`deny`

to block new deployments violating the baseline initiative. You can also add extra namespaces to exclude from evaluation. For this example, keep the default values. - Select
**Review + create**>**Create**to submit the policy assignment.

## Create and assign a custom policy definition

Custom policies allow you to define rules for using Azure. For example, you can enforce the following types of rules:

- Security practices
- Cost management
- Organization-specific rules (like naming or locations)

Before creating a custom policy, check the [list of common patterns and samples](/en-us/azure/governance/policy/samples/) to see if your case is already covered.

Custom policy definitions are written in JSON. To learn more about creating a custom policy, see [Azure Policy definition structure](/en-us/azure/governance/policy/concepts/definition-structure) and [Create a custom policy definition](/en-us/azure/governance/policy/tutorials/create-custom-policy-definition).

Note

Azure Policy now utilizes a new property known as *templateInfo* that allows you to define the source type for the constraint template. When you define *templateInfo* in policy definitions, you don’t have to define *constraintTemplate* or *constraint* properties. You still need to define *apiGroups* and *kinds*. For more information on this, see [Understanding Azure Policy effects](/en-us/azure/governance/policy/concepts/effects#audit-properties).

Once you create your custom policy definition, see [Assign a policy definition](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#assign-a-policy-definition) for a step-by-step walkthrough of assigning the policy to your Kubernetes cluster.

## Validate an Azure Policy is running

Confirm the policy assignments are applied to your cluster using the following

`kubectl get`

command.`kubectl get constrainttemplates`

Note

Policy assignments can take

[up to 20 minutes to sync](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#assign-a-policy-definition)into each cluster.Your output should be similar to the following example output:

`NAME AGE k8sazureallowedcapabilities 23m k8sazureallowedusersgroups 23m k8sazureblockhostnamespace 23m k8sazurecontainerallowedimages 23m k8sazurecontainerallowedports 23m k8sazurecontainerlimits 23m k8sazurecontainernoprivilege 23m k8sazurecontainernoprivilegeescalation 23m k8sazureenforceapparmor 23m k8sazurehostfilesystem 23m k8sazurehostnetworkingports 23m k8sazurereadonlyrootfilesystem 23m k8sazureserviceallowedports 23m`


### Validate rejection of a privileged pod

Let's first test what happens when you schedule a pod with the security context of `privileged: true`

. This security context escalates the pod's privileges. The initiative disallows privileged pods, so the request is denied, which results in the deployment being rejected.

Create a file named

`nginx-privileged.yaml`

and paste in the following YAML manifest.`apiVersion: v1 kind: Pod metadata: name: nginx-privileged spec: containers: - name: nginx-privileged image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine securityContext: privileged: true`

Create the pod using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f nginx-privileged.yaml`

As expected, the pod fails to be scheduled, as shown in the following example output:

`Error from server ([denied by azurepolicy-container-no-privilege-00edd87bf80f443fa51d10910255adbc4013d590bec3d290b4f48725d4dfbdf9] Privileged container is not allowed: nginx-privileged, securityContext: {"privileged": true}): error when creating "privileged.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [denied by azurepolicy-container-no-privilege-00edd87bf80f443fa51d10910255adbc4013d590bec3d290b4f48725d4dfbdf9] Privileged container is not allowed: nginx-privileged, securityContext: {"privileged": true}`

The pod doesn't reach the scheduling stage, so there are no resources to delete before you move on.


### Test creation of an unprivileged pod

In the previous example, the container image automatically tried to use root to bind NGINX to port 80. The policy initiative denies this request, so the pod fails to start. Now, let's try running that same NGINX pod without privileged access.

Create a file named

`nginx-unprivileged.yaml`

and paste in the following YAML manifest.`apiVersion: v1 kind: Pod metadata: name: nginx-unprivileged spec: containers: - name: nginx-unprivileged image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine`

Create the pod using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f nginx-unprivileged.yaml`

Check the status of the pod using the

command.`kubectl get pods`

`kubectl get pods`

Your output should be similar to the following example output, which shows the pod is successfully scheduled and has a status of

*Running*:`NAME READY STATUS RESTARTS AGE nginx-unprivileged 1/1 Running 0 18s`

This example shows the baseline initiative affecting only the deployments that violate policies in the collection. Allowed deployments continue to function.

Delete the NGINX unprivileged pod using the

command and specify the name of your YAML manifest.`kubectl delete`

`kubectl delete -f nginx-unprivileged.yaml`


## Disable a policy or initiative

You can remove the baseline initiative in the Azure portal using the following steps:

- Navigate to the
**Policy**pane on the Azure portal. - Select
**Assignments**. - Select the
**...**button next to the**Kubernetes cluster pod security baseline standards for Linux-based workload**initiative. - Select
**Delete assignment**.

## Next steps

For more information about how Azure Policy works, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-container-image-management -->

# Best practices for container image management and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container and container image security is a major priority when developing and running applications in Azure Kubernetes Service (AKS). Containers with outdated base images or unpatched application runtimes introduce security risks and possible attack vectors. You can minimize these risks by integrating and running scan and remediation tools in your containers at build and runtime. The earlier you catch the vulnerability or outdated base image, the more secure your application is.

In this article, *"containers"* refers to both the container images stored in a container registry and running containers.

This article focuses on how to secure your containers in AKS. You learn how to:

- Scan for and remediate image vulnerabilities.
- Automatically trigger and redeploy container images when a base image is updated.

- You can read the best practices for
[cluster security](operator-best-practices-cluster-security)and[pod security](developer-best-practices-pod-security). - You can use
[Container security in Defender for Cloud](/en-us/azure/security-center/container-security)to help scan your containers for vulnerabilities.[Azure Container Registry integration](/en-us/azure/security-center/defender-for-container-registries-introduction)with Defender for Cloud helps protect your images and registry from vulnerabilities.

## Secure the images and runtime


Best practice guidance

- Scan your container images for vulnerabilities.
- Only deploy validated images.
- Regularly update the base images and application runtime.
- Redeploy workloads in the AKS cluster.

When adopting container-based workloads, you want to verify the security of images and runtime used to build your own applications. To help avoid introducing security vulnerabilities into your deployments, you can use the following best practices:

- Include in your deployment workflow a process to scan container images using tools, such as
[Twistlock](https://www.twistlock.com/)or[Aqua](https://www.aquasec.com/). - Only allow verified images to be deployed.

For example, you can use a continuous integration and continuous deployment (CI/CD) pipeline to automate the image scans, verification, and deployments. Azure Container Registry includes these vulnerabilities scanning capabilities.

## Automatically build new images on base image update


Best practice guidanceAs you use base images for application images, use automation to build new images when the base image is updated. Since updated base images typically include security fixes, update any downstream application container images.


Each time a base image is updated, you should also update any downstream container images. Integrate this build process into validation and deployment pipelines such as [Azure Pipelines](/en-us/azure/devops/pipelines/) or Jenkins. These pipelines ensure your applications continue to run on the updated based images. Once your application container images are validated, you can then update AKS deployments to run the latest secure images.

Azure Container Registry Tasks can also automatically update container images when the base image is updated. With this feature, you build a few base images and keep them updated with bug and security fixes.

For more information about base image updates, see [Automate image builds on base image update with Azure Container Registry Tasks](/en-us/azure/container-registry/container-registry-tutorial-base-image-update).

## Next steps

This article focused on how to secure your containers. To implement some of these areas, see the following article:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/scale-cluster -->

# Manually scale the node count in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If the resource needs of your applications change, your cluster performance may be impacted due to low capacity on CPU, memory, PID space, or disk sizes. To address these changes, you can manually scale your AKS cluster to run a different number of nodes. When you scale in, nodes are carefully [cordoned and drained](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/) to minimize disruption to running applications. When you scale out, AKS waits until nodes are marked **Ready** by the Kubernetes cluster before pods are scheduled on them.

This article describes how to manually increase or decrease the number of nodes in an AKS cluster.

## Before you begin

Review the

[AKS service quotas and limits](quotas-skus-regions#service-quotas-and-limits)to verify your cluster can scale to your desired number of nodes.The name of a node pool may only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-11 characters.
- For Windows node pools, the length must be between 1-6 characters.


## Scale the cluster nodes

Important

Removing nodes from a node pool using the kubectl command isn't supported. Doing so can create scaling issues with your AKS cluster.

Get the

*name*of your node pool using thecommand. The following example gets the node pool name for the cluster named`az aks show`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks show --resource-group myResourceGroup --name myAKSCluster --query agentPoolProfiles`

The following example output shows that the

*name*is*nodepool1*:`[ { "count": 1, "maxPods": 110, "name": "nodepool1", "osDiskSizeGb": 30, "osType": "Linux", "vmSize": "Standard_DS2_v2" } ]`

Scale the cluster nodes using the

command. The following example scales a cluster named`az aks scale`

*myAKSCluster*to a single node. Provide your own`--nodepool-name`

from the previous command, such as*nodepool1*:`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 1 --nodepool-name <your node pool name>`

The following example output shows the cluster successfully scaled to one node, as shown in the

*agentPoolProfiles*section:`{ "aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { "count": 1, "maxPods": 110, "name": "nodepool1", "osDiskSizeGb": 30, "osType": "Linux", "vmSize": "Standard_DS2_v2", "vnetSubnetId": null } ], [...] }`


## Scale `User`

node pools to 0

Unlike `System`

node pools that always require running nodes, `User`

node pools allow you to scale to 0. To learn more on the differences between system and user node pools, see [System and user node pools](use-system-pools).

Important

You can't scale a user node pool with the cluster autoscaler enabled to 0 nodes. To scale a user node pool to 0 nodes, you must disable the cluster autoscaler first. For more information, see [Disable the cluster autoscaler on a node pool](cluster-autoscaler#disable-the-cluster-autoscaler-on-a-node-pool).

To scale a user pool to 0, you can use the

[az aks nodepool scale](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-scale)in alternative to the above`az aks scale`

command, and set`0`

as your node count.`az aks nodepool scale --name <your node pool name> --cluster-name myAKSCluster --resource-group myResourceGroup --node-count 0`

You can also autoscale

`User`

node pools to zero nodes, by setting the`--min-count`

parameter of the[Cluster Autoscaler](cluster-autoscaler)to`0`

.

## Next steps

In this article, you manually scaled an AKS cluster to increase or decrease the number of nodes. You can also use the [cluster autoscaler](cluster-autoscaler) to automatically scale your cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-aks-scheduler -->

# Configure advanced scheduler profiles on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy example scheduler profiles in Azure Kubernetes Service (AKS) to configure advanced scheduling behavior using in-tree scheduling plugins. This guide also explains how to verify the successful application of custom scheduler profiles targeting specific node pools or the entire AKS cluster.

## Limitations

- AKS currently doesn't manage the deployment of third-party schedulers or out-of-tree scheduling plugins.
- AKS doesn't support in-tree scheduling plugins targeting the
`aks-system`

scheduler. This restriction is in place to help prevent unexpected changes to AKS add-ons enabled on your cluster. Additionally, you can't define a`profile`

called`aks-system`

.

## Prerequisites

- The Azure CLI version
`2.76.0`

or later. Run`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version
`1.33`

or later running on your AKS cluster. - The
version`aks-preview`

Azure CLI extension`18.0.0b27`

or later. [Register the](#register-the-user-defined-scheduler-configuration-preview-feature-flag)in your Azure subscription.`UserDefinedSchedulerConfigurationPreview`

feature flag- Review the
[supported advanced scheduling concepts](concepts-scheduler-configuration)and in-tree scheduling plugins on AKS.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the

`aks-preview`

extension using thecommand.`az extension update`

`az extension update --name aks-preview`


### Register the User Defined Scheduler Configuration Preview feature flag

Register the

`UserDefinedSchedulerConfigurationPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "UserDefinedSchedulerConfigurationPreview"`

It takes a few minutes for the status to show

*Registered*.When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable scheduler profile configuration on an AKS cluster

You can enable schedule profile configuration on a new or existing AKS cluster.

Create an AKS cluster with scheduler profile configuration enabled using the

command with the`az aks create`

`--enable-upstream-kubescheduler-user-configuration`

flag.`# Set environment variables export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<aks-cluster-name> # Create an AKS cluster with schedule profile configuration enabled az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-upstream-kubescheduler-user-configuration \ --generate-ssh-keys`

Once the creation process completes, connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify installation of the scheduler controller

After enabling the feature on your AKS cluster, verify the custom resource definition (CRD) of the scheduler controller was successfully installed using the

`kubectl get`

command.`kubectl get crd schedulerconfigurations.aks.azure.com`

Note

This command won't succeed if the feature wasn't successfully enabled in the

[previous section](#enable-scheduler-profile-configuration-on-an-aks-cluster).

## Configure node bin-packing

Node bin-packing is a scheduling strategy that maximizes resource utilization by increasing pod density on nodes, within the set configuration. This strategy helps improve cluster efficiency by minimizing wasted resources and lowering the operational cost of maintaining idle or underutilized nodes.

In this example, the configured scheduler prioritizes scheduling pods on nodes with high CPU usage. Explicitly, this configuration avoids underutilizing nodes that still have free resources and helps to make better use of the resources already allocated to nodes. The CRD must be named `upstream`

.

Create a file named

`bin-pack-cpu-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: node-binpacking-cpu-scheduler pluginConfig: - name: NodeResourcesFit args: scoringStrategy: type: MostAllocated resources: - name: cpu weight: 1`

`NodeResourcesFit`

ensures that the scheduler checks if a node has enough resources to run the pod.`scoringStrategy: MostAllocated`

tells the scheduler to prefer nodes with high CPU resource usage. This helps achieve**better resource utilization**by placing new pods on nodes that are already "highly used".`Resources`

specifies that`CPU`

is the primary resource being considered for scoring, and with a weight of`1`

, CPU usage is prioritized with a relatively equal level of importance in the scheduling decision.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f bin-pack-cpu-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: node-binpacking-cpu-scheduler ... ...`


## Configure pod topology spread

Pod topology spread is a scheduling strategy that seeks to distribute pods evenly across failure domains (such as availability zones or regions) to ensure high availability and fault tolerance in the event of zone or node failures. This strategy helps prevent the risk of all replicas of a pod being placed in the same failure domain. For more configuration guidance, see the [Kubernetes Pod Topology Spread Constraints documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/). The CRD must be named `upstream`

.

Create a file named

`pod-topology-spreader-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: pod-distribution-scheduler pluginConfig: - name: PodTopologySpread args: apiVersion: kubescheduler.config.k8s.io/v1 kind: PodTopologySpreadArgs defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: ScheduleAnyway`

`PodTopologySpread`

plugin instructs the scheduler to try and distribute pods as evenly as possible across availability zones.`whenUnsatisfiable: ScheduleAnyway`

specifies schedule to schedule pods despite the inability to meet the topology constraints. This avoids pod scheduling failures when exact distribution isn't feasible.`List`

type applies the default constraints as a list of rules. The scheduler uses the rules in the order they're defined, and they apply to all pods that don’t specify custom topology spread constraints.`maxSkew: 1`

means the number of pods can differ by at most*1*between any two availability zones.`topologyKey: topology.kubernetes.io/zone`

indicates that the scheduler should spread pods across availability zones.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f pod-topology-spreader-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: pod-distribution-scheduler ... ...`


## Assign a scheduler profile to an entire AKS cluster

In your scheduler profile configuration, update the

`schedulerName`

field as follows:`... ... - schedulerName: default_scheduler ... ...`

Reapply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`

Now, this configuration will become the

**default**scheduling operation for your entire AKS cluster.

## Configure multiple scheduler profiles

You can customize the upstream scheduler with multiple profiles and customize each profile with multiple plugins while using the same configuration file. As a reminder, the CRD must be named `upstream`

and user-configured fields include `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, and `profiles`

.

In the following example, we create two scheduling profiles called **scheduler-one** and **scheduler-two**. The fields `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, apply globally to all profiles defined.

**global parameters**

`percentageOfNodesToScore`

specifies the percentage of cluster nodes the scheduler evaluates during scoring to balance scheduling accuracy and speed. So**percentageOfNodesToScore: 40**means the scheduler will sample 40% of nodes instead of the entire cluster.`podInitialBackoffSeconds`

defines the initial delay before retrying a failed scheduling attempt to prevent rapid, repeated retries. So**podInitialBackoffSeconds: 1**means the scheduler waits 1 second before the first retry.`podMaxBackoffSeconds`

sets the maximum delay the scheduler will wait between exponential backoff retries for unschedulable pods. So**podMaxBackoffSeconds: 8**means the retry delay will never exceed 8 seconds even as backoff increases.

**scheduler-one** prioritizes placing pods across zones and nodes for balanced distribution with the following settings:

- Enforces strict zonal distribution and
*preferred*node distribution using`PodTopologySpread`

. - Honors hard pod affinity rules and considers the soft affinity rules with
`InterPodAffinity`

. *Prefers*nodes in specific zones to reduce cross-zone networking using`NodeAffinity`

.

**scheduler-two** prioritizes placing pods on nodes with available storage, CPU, and memory resources for timely resource-efficient resource usage with the following settings:

- Ensures pods are placed on nodes where PVCs can bind to PVs using
`VolumeBinding`

. - Validates that nodes and volumes satisfy zonal requirements using
`VolumeZone`

to avoid cross-zone storage access. - Prioritizes nodes based on CPU, memory, and ephemeral storage utilization, with
`NodeResourcesFit`

. - Favors nodes that already have the required container images using
`ImageLocality`

.

Note

You might need to adjust zones and other parameters based on your workload type.

Create a file named

`aks-scheduler-customization.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration percentageOfNodesToScore: 40 podInitialBackoffSeconds: 1 podMaxBackoffSeconds: 8 profiles: - schedulerName: scheduler-one plugins: multiPoint: enabled: - name: PodTopologySpread - name: InterPodAffinity - name: NodeAffinity pluginConfig: # PodTopologySpread with strict zonal distribution - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 2 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: ScheduleAnyway - name: InterPodAffinity args: hardPodAffinityWeight: 1 ignorePreferredTermsOfExistingPods: false - name: NodeAffinity args: addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2, westus3-3] - schedulerName: scheduler-two plugins: multiPoint: enabled: - name: VolumeBinding - name: VolumeZone - name: NodeAffinity - name: NodeResourcesFit - name: PodTopologySpread - name: ImageLocality pluginConfig: - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: DoNotSchedule - name: VolumeBinding args: apiVersion: kubescheduler.config.k8s.io/v1 kind: VolumeBindingArgs bindTimeoutSeconds: 300 - name: NodeAffinity args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeAffinityArgs addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2] - name: NodeResourcesFit args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeResourcesFitArgs scoringStrategy: type: MostAllocated resources: - name: cpu weight: 3 - name: memory weight: 1 - name: ephemeral-storage weight: 2`

Apply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`


## Disable an AKS scheduler profile configuration

To disable the AKS scheduler profile configuration and revert to AKS scheduler default configuration on the cluster, first delete the

`schedulerconfiguration`

resource using the`kubectl delete`

command.`kubectl delete schedulerconfiguration upstream || true`

Note

Ensure that the previous step is complete and confirm that the

`schedulerconfiguration`

resource was deleted before proceeding to disable this feature.Disable the feature using the

command with the`az aks update`

`--disable-upstream-kubescheduler-user-configuration`

flag.`az aks update --subscription="${SUBSCRIPTION_ID}" \ --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --disable-upstream-kubescheduler-user-configuration`

Verify the feature is disabled using the

command.`az aks show`

`az aks show --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --query='properties.schedulerProfile'`

Your output should indicate that the feature is no longer enabled on your AKS cluster.


## Frequently asked questions (FAQ)

### What happens if I apply misconfigured scheduler profile to my AKS cluster?

Once you apply a scheduler profile, AKS checks if it contains a valid configuration of plugins and arguments. If the configuration targets a disallowed scheduler or sets the in-tree scheduling plugins improperly, AKS rejects the configuration and reverts to the last known "accepted" scheduler configuration. This check aims to limit impact on new and existing AKS clusters due to scheduler misconfiguration.

### How can I monitor and validate that the scheduler honored my configuration?

There are *three* recommended methods for observing the results of your applied scheduler profile:

- View the AKS
`kube-scheduler`

control plane logs to ensure that the scheduler received the configuration from the CRD. - Run the
`kubectl get schedulerconfiguration`

command. The output displays the status of the`configuration: pending`

during the rollout and`Succeeded`

or`Failed`

after the configuration is accepted or rejected by the scheduler. - Run the
`kubectl describe schedulerconfiguration`

command. The output displays a more detailed state of the scheduler, including any error during the reconciliation, and the current scheduler configuration in effect.

## Next steps

To learn more about the AKS scheduler and best practices, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-storage-drivers -->

# Container Storage Interface (CSI) drivers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Kubernetes. By adopting and using CSI, Azure Kubernetes Service (AKS) can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes without having to touch the core Kubernetes code and wait for its release cycles.

The CSI storage driver support on AKS allows you to natively use:

can be used to create a Kubernetes**Azure Disks***DataDisk*resource. Disks can use Azure Premium Storage, backed by high-performance SSDs, or Azure Standard Storage, backed by regular HDDs or Standard SSDs. For most production and development workloads, use Premium Storage. Azure Disks are mounted as*ReadWriteOnce*and are only available to one node in AKS. For storage volumes that can be accessed by multiple nodes simultaneously, use Azure Files.can be used to mount an SMB 3.0/3.1 share backed by an Azure storage account to pods. With Azure Files, you can share data across multiple nodes and pods. Azure Files can use Azure Standard storage backed by regular HDDs or Azure Premium storage backed by high-performance SSDs.**Azure Files**can be used to mount Blob storage (or object storage) as a file system into a container or pod. Using Blob storage enables your cluster to support applications that work with large unstructured datasets like log file data, images or documents, HPC, and others. Additionally, if you ingest data into**Azure Blob storage**[Azure Data Lake storage](/en-us/azure/storage/blobs/data-lake-storage-introduction), you can directly mount and use it in AKS without configuring another interim filesystem.

Tip

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Prerequisites

- You need the Azure CLI version 2.42 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If the open-source CSI storage driver is installed on your cluster, uninstall it before enabling the Azure storage CSI driver.
- To enforce the Azure Policy for AKS
[policy definition](/en-us/azure/governance/policy/samples/built-in-policies#kubernetes)**Kubernetes clusters should use Container Storage Interface(CSI) driver StorageClass**, the Azure Policy add-on needs to be enabled on new and existing clusters. For an existing cluster, review the[Learn Azure Policy for Kubernetes](/en-us/azure/governance/policy/concepts/policy-for-kubernetes)to enable it.

## Disk encryption supported scenarios

CSI storage drivers support the following scenarios:

[Encrypted managed disks with customer-managed keys](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys)using Azure Key Vaults stored in a different Microsoft Entra tenant.- Encrypt your Azure Storage disks hosting AKS OS and application data with
[customer-managed keys](azure-disk-customer-managed-keys).

## Enable CSI storage drivers on an existing cluster

To enable CSI storage drivers on a new cluster, include one of the following parameters depending on the storage system:

`--enable-disk-driver`

allows you to enable the[Azure Disks CSI driver](azure-disk-csi).`--enable-file-driver`

allows you to enable the[Azure Files CSI driver](azure-files-csi).`--enable-blob-driver`

allows you to enable the[Azure Blob storage CSI driver](azure-blob-csi).`--enable-snapshot-controller`

allows you to enable the[snapshot controller](https://kubernetes-csi.github.io/docs/snapshot-controller.html).

```
az aks update --name myAKSCluster --resource-group myResourceGroup --enable-disk-driver --enable-file-driver --enable-blob-driver --enable-snapshot-controller
```


It might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results when enabling the Blob storage CSI driver:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
```


## Disable CSI storage drivers on a new or existing cluster

To disable CSI storage drivers on a new cluster, include one of the following parameters depending on the storage system:

`--disable-disk-driver`

allows you to disable the[Azure Disks CSI driver](azure-disk-csi).`--disable-file-driver`

allows you to disable the[Azure Files CSI driver](azure-files-csi).`--disable-blob-driver`

allows you to disable the[Azure Blob storage CSI driver](azure-blob-csi).`--disable-snapshot-controller`

allows you to disable the[snapshot controller](https://kubernetes-csi.github.io/docs/snapshot-controller.html).

```
az aks create \
--name myAKSCluster \
--resource-group myResourceGroup \
--disable-disk-driver \
--disable-file-driver \
--disable-blob-driver \
--disable-snapshot-controller \
--generate-ssh-keys
```


To disable CSI storage drivers on an existing cluster, use one of the parameters listed earlier depending on the storage system:

```
az aks update \
--name myAKSCluster \
--resource-group myResourceGroup \
--disable-disk-driver \
--disable-file-driver \
--disable-blob-driver \
--disable-snapshot-controller
```


Note

We recommend deleting the corresponding PersistentVolumeClaim object instead of the PersistentVolume object when deleting a CSI volume. The external provisioner in the CSI driver will react to the deletion of the PersistentVolumeClaim and based on its reclamation policy, it issues the DeleteVolume call against the CSI volume driver commands to delete the volume. The PersistentVolume object is then deleted.

## Migrate custom in-tree storage classes to CSI

Starting with Kubernetes version 1.26, in-tree persistent volume types *kubernetes.io/azure-disk* and *kubernetes.io/azure-file* are deprecated and will no longer be supported. *In-tree drivers* refers to the storage drivers that are part of the core Kubernetes code opposed to the CSI drivers, which are plug-ins.

Removing these drivers following their deprecation isn't planned, however you should migrate to the corresponding CSI drivers *disk.csi.azure.com* and *file.csi.azure.com*. To review the migration options for your storage classes and upgrade your cluster to use Azure Disks and Azure Files CSI drivers, see [Migrate from in-tree to CSI drivers](csi-migrate-in-tree-volumes).

If you've created in-tree driver storage classes, those storage classes continue to work since CSI migration is turned on after upgrading your cluster to 1.21.x. If you want to use CSI features you'll need to perform the migration.

## Next steps

- To use the CSI driver for Azure Disks, see
[Use Azure Disks with CSI drivers](azure-disk-csi). - To use the CSI driver for Azure Files, see
[Use Azure Files with CSI drivers](azure-files-csi). - To use the CSI driver for Azure Blob storage, see
[Use Azure Blob storage with CSI drivers](azure-blob-csi) - For more about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information on CSI migration, see
[Kubernetes in-tree to CSI Volume Migration](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-csi-migration-beta).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/resize-node-pool -->

# Resize node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might want to change the size of your virtual machines (VMs) to accommodate an increasing number of deployments or to run a larger workload. Resizing AKS instances directly isn't supported when using [Virtual Machine Scale Sets](/en-us/azure/virtual-machine-scale-sets/overview) in AKS, as outlined in the [support policies for AKS](support-policies#user-customization-of-agent-nodes):

AKS agent nodes appear in the Azure portal as regular Azure IaaS resources. But these virtual machines are deployed into a custom Azure resource group (usually prefixed with MC_*). You can't make direct customizations to these nodes using the IaaS APIs or resources. Any custom changes that aren't done via the AKS API won't persist through an upgrade, scale, update, or reboot.


In this article, you learn the recommended method to resize a node pool by creating a new node pool with the desired SKU size, cordoning and draining the existing nodes, and then removing the existing node pool.

Important

This method is specific to [Virtual Machine Scale Sets](/en-us/azure/virtual-machine-scale-sets/overview)-based AKS clusters. When using Virtual Machines-based node pools, you can easily update the VM sizes in an existing node pool using a single Azure CLI command and have multiple VM sizes in the same node pool. For more information, see the [Virtual Machines node pools documentation](virtual-machines-node-pools).

## Create a new node pool with the desired SKU

Note

Every AKS cluster must contain at least one system node pool with at least one node. In this example, we use a `--mode`

of `System`

to add a system node pool to replace the system node pool we want to resize. You can [update the mode of a node pool](use-system-pools#update-existing-cluster-system-and-user-node-pools) at any time. You can also add a user node pool by setting `--mode`

to `User`

.

When resizing, make sure you consider all workload requirements, such as availability zones, and configure your VMSS node pool accordingly. You might need to modify the following command to best fit your needs. For a full list of the configuration options, see the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) reference page.

Create a new node pool using the

command. In this example, we create a new node pool,`az aks nodepool add`

`mynodepool`

, with three nodes and the`Standard_DS3_v2`

VM SKU to replace an existing node pool,`nodepool1`

, that has the`Standard_DS2_v2`

VM SKU.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 3 \ --node-vm-size Standard_DS3_v2 \ --mode System \ --no-wait`

It takes a few minutes for the new node pool to be created.

Get the status of the new node pool using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing both the new node pool

`mynodepool`

and the existing node pool`nodepool1`

:`NAME STATUS ROLES AGE VERSION aks-mynodepool-98765432-vmss000000 Ready agent 23m v1.21.9 aks-mynodepool-98765432-vmss000001 Ready agent 23m v1.21.9 aks-mynodepool-98765432-vmss000002 Ready agent 23m v1.21.9 aks-nodepool1-12345678-vmss000000 Ready agent 10d v1.21.9 aks-nodepool1-12345678-vmss000001 Ready agent 10d v1.21.9 aks-nodepool1-12345678-vmss000002 Ready agent 10d v1.21.9`


## Cordon the existing nodes

Cordoning marks specified nodes as unschedulable and prevents any more pods from being added to the nodes.

Get the names of the nodes you want to cordon using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing the nodes in the existing node pool

`nodepool1`

that you want to cordon:`NAME STATUS ROLES AGE VERSION aks-nodepool1-12345678-vmss000000 Ready agent 7d21h v1.21.9 aks-nodepool1-12345678-vmss000001 Ready agent 7d21h v1.21.9 aks-nodepool1-12345678-vmss000002 Ready agent 7d21h v1.21.9`

Cordon the existing nodes using the

`kubectl cordon`

command, specifying the desired nodes in a space-separated list. For example:`kubectl cordon aks-nodepool1-12345678-vmss000000 aks-nodepool1-12345678-vmss000001 aks-nodepool1-12345678-vmss000002`

Your output should resemble the following example output, showing that the nodes are cordoned:

`node/aks-nodepool1-12345678-vmss000000 cordoned node/aks-nodepool1-12345678-vmss000001 cordoned node/aks-nodepool1-12345678-vmss000002 cordoned`


## Drain the existing nodes

Important

To successfully drain nodes and evict running pods, ensure that any PodDisruptionBudgets (PDBs) allow for at least one pod replica to be moved at a time. Otherwise, the drain/evict operation fails. To check this, you can run `kubectl get pdb -A`

and verify `ALLOWED DISRUPTIONS`

is at least `1`

or higher.

When you drain nodes, the pods running on them are evicted and recreated on the other schedulable nodes.

Drain the existing nodes using the

`kubectl drain`

command with the`--ignore-daemonsets`

and`--delete-emptydir-data`

flags, specifying the desired nodes in a space-separated list. For example:Important

Using

`--delete-emptydir-data`

is required to evict the AKS-created`coredns`

and`metrics-server`

pods. If you don't use this flag, you get an error. For more information, see the[documentation on emptydir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir).`kubectl drain aks-nodepool1-12345678-vmss000000 aks-nodepool1-12345678-vmss000001 aks-nodepool1-12345678-vmss000002 --ignore-daemonsets --delete-emptydir-data`

After the drain operation finishes, all pods (excluding the pods controlled by daemon sets) should be running on the new node pool. You can verify this using the

`kubectl get pods`

command.`kubectl get pods -o wide -A`


### Troubleshoot pod eviction issues

You might encounter the following error when draining nodes:


`Error when evicting pods/[podname] -n [namespace] (will retry after 5s): Cannot evict pod as it would violate the pod's disruption budget.`


By default, your cluster has AKS-managed pod disruption budgets (such as `coredns-pdb`

or `konnectivity-agent`

) with a `MinAvailable`

of `1`

. For example, if there are two `coredns`

pods running, only one can be disrupted at a time. While one of them is getting recreated and is unavailable, the other `coredns`

pod can't be evicted due to the pod disruption budget. This issue resolves itself after the initial `coredns`

pod is scheduled and running, allowing the second pod to be properly evicted and recreated.

Tip

Consider draining nodes one by one for a smoother eviction experience and to avoid throttling. For more information, see:

## Remove the existing node pool

Important

When you delete a node pool, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the node pool you plan to delete, perform a cordon and drain on all nodes in the node pool before deleting.

Delete the original node pool using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1`

Verify that your AKS cluster has only the new node pool with the applications and pods properly running using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing only the new node pool

`mynodepool`

:`NAME STATUS ROLES AGE VERSION aks-mynodepool-98765432-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-98765432-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-98765432-vmss000002 Ready agent 63m v1.21.9`


## Next steps

After resizing a node pool by cordoning and draining, learn more about [using multiple node pools](create-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ray-overview -->

# Deploy a Ray cluster on Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy a Ray cluster on Azure Kubernetes Service (AKS) using the KubeRay operator. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What is Ray?

[Ray](https://docs.ray.io/en/latest/index.html#) is an open-source project developed at UC Berkeley's RISE Lab that provides a unified framework for scaling AI and Python applications. It consists of a core distributed runtime and a set of AI libraries designed to accelerate machine learning workloads.

Ray simplifies the process of running compute-intensive Python tasks at scale, allowing you to seamlessly scale your applications. The framework supports various machine learning tasks, including distributed training, hyperparameter tuning, reinforcement learning, and production model serving.

For more information, see the [Ray GitHub repository](https://github.com/ray-project/ray).

## What is KubeRay?

[KubeRay](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started.html) is an open-source Kubernetes operator for deploying and managing Ray clusters on Kubernetes. KubeRay automates the deployment, scaling, and monitoring of Ray clusters. It provides a declarative way to define Ray clusters using Kubernetes custom resources, making it easy to manage Ray clusters alongside other Kubernetes resources.

For more information, see the [KubeRay GitHub repository](https://github.com/ray-project/kuberay).

## Ray deployment process

The deployment process consists of the following steps:

- Use Terraform to create a local plan file to define the desired state for infrastructure required AKS infrastructure that consists of an Azure resource group, a dedicated system node pool, and a workload node pool for Ray with three nodes.
- Deploy a local Terraform plan to Azure.
- Retrieve outputs from the Terraform deployment and obtain Kubernetes credentials to the newly deployed AKS cluster.
- Install the Helm Ray repository and deploy KubeRay to the AKS cluster using Helm.
- Download and execute a
[Ray Job](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/index.html)YAML manifest from the Ray GitHub samples repo to perform an image classification with a[MNIST](https://github.com/cvdfoundation/mnist)dataset using[Convolutional Neural Networks (CNNs)](https://techcommunity.microsoft.com/discussions/machinelearning/what-is-convolutional-neural-network-%E2%80%94-cnn-deep-learning/4184725). - Output the logs from the Ray Job to gain insight into the machine learning process performed by Ray.

## Next step

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-migration -->

# Migrate from Dapr OSS to the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to migrate from Dapr OSS to the Dapr extension for AKS.

You can configure the Dapr extension to use and manage the Kubernetes resources created by Dapr OSS by either:

[Checking for an existing Dapr installation using the Azure CLI](#check-for-an-existing-dapr-installation)(*default method*), or[Configuring the existing Dapr installation using](#configure-the-existing-dapr-installation-using---configuration-settings).`--configuration-settings`


For more information, see [an overview of the Dapr extension for AKS](dapr-overview).

## Check for an existing Dapr installation

When you [install the Dapr extension](dapr), the extension checks for an existing Dapr installation on your cluster. If Dapr exists, the extension uses and manages the Kubernetes resources created by Dapr OSS.

List the details of your current Dapr installation using the

`helm list -A`

command and save the Dapr release name and namespace from the output.`helm list -A`

Enter the Helm release name and namespace (from

`helm list -A`

) when prompted with the following questions:`Enter the Helm release name for Dapr, or press Enter to use the default name [dapr]: Enter the namespace where Dapr is installed, or press Enter to use the default namespace [dapr-system]:`


## Configure the existing Dapr installation using `--configuration-settings`


When you [create the Dapr extension](dapr), you can configure the extension to use and manage the Kubernetes resources created by Dapr OSS using the `--configuration-settings`

flag.

List the details of your current Dapr installation using the

`helm list -A`

command and save the Dapr release name and namespace from the output.`helm list -A`

Create the Dapr extension using the

and use the`az k8s-extension create`

`--configuration-settings`

flags to set the Dapr release name and namespace.`az k8s-extension create --cluster-type managedClusters \ --cluster-name myAKSCluster \ --resource-group myResourceGroup \ --name dapr \ --extension-type Microsoft.Dapr \ --configuration-settings "existingDaprReleaseName=dapr" \ --configuration-settings "existingDaprReleaseNamespace=dapr-system"`


## Update HA mode or placement service settings

When installing the Dapr extension on top of an existing Dapr installation, you receive the following message:

```
The extension will be installed on your existing Dapr installation. Note, if you have updated the default values for global.ha.* or dapr_placement.* in your existing Dapr installation, you must provide them in the configuration settings. Failing to do so will result in an error, since Helm upgrade will try to modify the StatefulSet. See <link> for more information.
```


Kubernetes only allows patching for limited fields in StatefulSets. If any of the HA mode or placement service settings are configured, the upgrade fails. To update the HA mode or placement service settings, you must delete the stateful set and then update the HA mode.

Delete the stateful set using the

`kubectl delete`

command.`kubectl delete statefulset.apps/dapr-placement-server -n dapr-system`

Update the HA mode using the

command.`az k8s-extension update`

`az k8s-extension update --cluster-type managedClusters \ --cluster-name myAKSCluster \ --resource-group myResourceGroup \ --name dapr \ --extension-type Microsoft.Dapr \ --auto-upgrade-minor-version true \ --configuration-settings "global.ha.enabled=true" \`


For more information, see the [Dapr production guidelines](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production/#enabling-high-availability-in-an-existing-dapr-deployment).

## Next steps

Learn more about [Dapr](dapr-overview) and [how to use it](dapr).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-annual-channel -->

# Use Windows Server Annual Channel for Containers on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS supports [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) in public preview. Each channel version is released annually and is supported for *two years*. This channel is beneficial if you require increased innovation cycles and portability.

Windows Server Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next, you can [upgrade to a Kubernetes version](upgrade-aks-cluster) that supports the next Annual Channel version.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Supported Annual Channel releases

AKS releases support for new releases of Windows Server Annual Channel for Containers in alignment with Kubernetes versions. For the latest updates, see the [AKS release notes](https://github.com/Azure/AKS/releases). The following table provides an *estimated* release schedule for upcoming Annual Channel releases:

| K8s version | Annual Channel (host) version | Container image supported | End of support date |
|---|---|---|---|
| 1.28 | 23H2 (preview only) | Windows Server 2022 | End of 1.33 support |
| 1.34 | 24H2 | Windows Server 2022 & Windows Server 2025 | End of 1.35 support |

## Windows Server Annual Channel vs. Long Term Servicing Channel Releases (LTSC)

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025, Windows Server 2022, and Windows Server 2019. These come from a different release channel than Windows Server Annual Channel for Containers. To view our current recommendations, see the [Windows best practices documentation](windows-best-practices).

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes][aks-release-notes]. To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

The following table compares Windows Server Annual Channel and Long Term Servicing Channel releases:

| Channel | Support | Upgrades |
|---|---|---|
| Long Term Servicing Channel (LTSC) | LTSC channels are released every three years and are supported for five years. This channel is recommended for customers using Long Term Support. | To upgrade from one release to the next, you need to migrate your node pools to a new OS SKU option and rebuild your container images with the new OS version. |
| Windows Server Annual Channel for Containers | Annual Channel releases occur annually and are supported for two years. | To upgrade to the latest release, you can upgrade the Kubernetes version of your node pool. |

## Before you begin

- You need the Azure CLI version 2.56.0 or later installed and configured to set
`os-sku`

to`WindowsAnnual`

with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- Windows Server Annual Channel doesn't support Azure Network Policy Manager.

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `AKSWindowsAnnualPreview`

feature flag

Register the

`AKSWindowsAnnualPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSWindowsAnnualPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AKSWindowsAnnualPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Use Windows Server Annual Channel for Containers on AKS

To use Windows Server Annual Channel on AKS, specify the following parameters:

`os-type`

set to`Windows`

`os-sku`

set to`WindowsAnnual`


Windows Server Annual Channel versions are based on the Kubernetes version of your node pool. To check which release you'll get based on the Kubernetes version of your node pool, see the [supported Annual Channel releases](#supported-annual-channel-releases).

### Create a new Windows Server Annual Channel node pool

Create a Windows Server Annual Channel node pool using the

command. The following example creates a Windows Server Annual Channel node pool with the 23H2 release:`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --os-sku WindowsAnnual \ --kubernetes-version 1.29 --name $NODE_POOL_NAME \ --node-count 1`

Note

If you don't specify the Kubernetes version during node pool creation, AKS uses the same Kubernetes version as your cluster.


### Verify Windows Server Annual Channel node pool creation

Verify Windows Server Annual Channel node pool creation by checking the OS SKU of your node pool using

`kubectl describe node`

command.`kubectl describe node $NODE_POOL_NAME`

If you successfully created a Windows Server Annual Channel node pool, you should see the following output:

`Name: npwin Roles: agent Labels: agentpool=npwin ... kubernetes.azure.com/os=windows ... kubernetes.azure.com/node-image-version=AKSWindows-23H2-gen2 ... kubernetes.azure.com/os-sku=WindowsAnnual`


### Upgrade an existing node pool to Windows Server Annual Channel

You can upgrade an existing node pool from an LTSC release to Windows Server Annual Channel by following the guidance in [Upgrade the OS version for your Azure Kubernetes Service (AKS) Windows workloads](upgrade-windows-os).

To upgrade from one Annual Channel version to the next, you can [upgrade to a Kubernetes version](upgrade-aks-cluster) that supports the next Annual Channel version.

## Next steps

To learn more about Windows Containers on AKS, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/supported-kubernetes-versions -->

# Supported Kubernetes versions in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community [releases minor versions](https://kubernetes.io/releases/) roughly every four months.

Minor version releases include new features and improvements. Patch releases are more frequent (sometimes weekly) and are intended for critical bug fixes within a minor version. Patch releases include fixes for security vulnerabilities or major bugs.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Kubernetes versions

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme for each version:

```
[major].[minor].[patch]
Examples:
1.29.2
1.29.1
```


Each number in the version reflects compatibility with previous versions:

**Major versions**: Introduce incompatible API changes or break backward compatibility.**Minor versions**: Add new features while maintaining backward compatibility.**Patch versions**: Include backward-compatible bug fixes.

Always use the latest patch release for your current minor version. For example, if your production cluster is on ** 1.29.1** and

**is the latest available patch version available for the**

`1.29.2`

*1.29*minor version, you should upgrade to

**as soon as possible to ensure your cluster is fully patched and supported.**

`1.29.2`

## AKS Kubernetes release calendar

Check the AKS Kubernetes release calendar for upcoming version releases. To see real-time updates of region release status and version release notes, visit the [AKS release status webpage](https://releases.aks.azure.com/). To learn more about the release status webpage, see [AKS release tracker](release-tracker).

Note

Note

AKS follows a 12-month support policy for generally available (GA) Kubernetes versions. To learn more about our Kubernetes version support policy, see the [FAQ](supported-kubernetes-versions#faq). Unless an explicit date is provided, the End of Life (EOL) date is the last day of the specified month. For example, "Mar 2026" indicates March 31, 2026.

For the past release history, see [Kubernetes history](https://github.com/kubernetes/kubernetes/releases).

| K8s version | Upstream release | AKS preview | AKS GA | End of life | Platform support |
|---|---|---|---|---|---|
| 1.29 | Dec 2023 | Feb 2024 | Mar 2024 | Mar 2025 | Until 1.33 GA |
| 1.30 | Apr 2024 | Jun 2024 | Jul 2024 | Aug 22, 2025 | Until 1.34 GA |
| 1.31 | Aug 2024 | Oct 2024 | Nov 2024 | Nov 1, 2025 | Until 1.35 GA |
| 1.32 | Dec 2024 | Feb 2025 | Apr 2025 | Mar 2026 | Until 1.36 GA |
| 1.33 | Apr 2025 | May 2025 | Jun 2025 | Jun 2026 | Until 1.37 GA |
| 1.34 | Aug 2025 | Oct 2025 | Nov 2025 | Nov 2026 | Until 1.38 GA |
| 1.35 | Dec 2025 | Feb 2026 | Mar 2026 | Mar 2027 | Until 1.39 GA |

### LTS Versions

Long-term support (LTS) needs to be enabled in order to get extended support. You can find more information on [Enable long-term support](/en-us/azure/aks/long-term-support#enable-long-term-support).

Note

Azure Linux 2.0 goes End of Life during the LTS period of AKS v1.28–v1.31. For more information on upgrading to Azure Linux 3.0 on AKS v1.28–v1.31, read the [Azure Linux AKS LTS Releases](/en-us/azure/azure-linux/support-cycle#aks-lts-releases) section.

| K8s version | Upstream release | AKS preview | AKS GA | End of life | LTS End of life |
|---|---|---|---|---|---|
| 1.27 | Apr 2023 | Jun 2023 | Jul 2023 | Jul 2024 | Jul 2025 |
| 1.28 | Aug 2023 | Sep 2023 | Nov 2023 | Jan 2025 | Feb 2026 |
| 1.29 | Dec 2023 | Feb 2024 | Mar 2024 | Mar 2025 | Apr 2026 |
| 1.30 | Apr 2024 | Jun 2024 | Jul 2024 | Aug 22, 2025 | Jul 2026 |
| 1.31 | Aug 2024 | Oct 2024 | Nov 2024 | Nov 1, 2025 | Nov 2026 |
| 1.32 | Dec 2024 | Feb 2025 | Apr 2025 | Mar 2026 | Mar 2027 |
| 1.33 | Apr 2025 | May 2025 | Jun 2025 | Jun 2026 | Jun 2027 |
| 1.34 | Aug 2025 | Oct 2025 | Nov 2025 | Nov 2026 | Nov 2027 |
| 1.35 | Dec 2025 | Feb 2026 | Mar 2026 | Mar 2027 | Mar 2028 |

### AKS Kubernetes release schedule Gantt chart

If you prefer to see this information visually, here's a Gantt chart with all the current releases displayed:

## AKS components breaking changes by version

Note the following important changes before you upgrade to any of the available minor versions:

### Kubernetes 1.34

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes From Kubernetes 1.33.0 |
Notes |
|---|---|---|---|---|
| aci-connector-linux 1.6.2 | addon-override-manager master.251002.2 | Linux - Ubuntu 22.04 |
kube-egress-gateway-daemon v0.0.21 → v0.1.3 | |
| addon-resizer v1.8.23-7 | apiserver-network-proxy-server v0.31.4-3 | azure-acr-credential-provider-pmc 1.34.1-ubuntu22.04u3 | kube-egress-gateway-daemon-init v0.0.21 → v0.1.3 | |
| ai-toolchain-operator 0.6.0 | app-routing-operator 0.2.12 | containerd 1.7.29-ubuntu22.04u1 | kube-egress-gateway-cnimanager v0.0.21 → v0.1.3 | |
| aks-windows-gpu-device-plugin 0.0.19 | automatic-authz-webhook master.251112.4 | datacenter-gpu-manager-4-core 1:4.4.1-1 | kube-egress-gateway-cni v0.0.21 → v0.1.3 | |
| ama-logs-linux 3.1.31 | ccp-webhook master.251105.4 | datacenter-gpu-manager-4-proprietary 1:4.4.1-1 | kube-egress-gateway-cni-ipam v0.0.21 → v0.1.3 | |
| ama-logs-win win-3.1.31 | cluster-autoscaler v1.33.1-aks-3 | kubectl 1.34.1-ubuntu22.04u4 | cloud-provider-node-manager-windows v1.33.3 → v1.34.0 | |
| app-routing-operator 0.0.3 | cost-analysis-scraper v0.0.25 | kubelet 1.34.1-ubuntu22.04u4 | cloud-provider-node-manager-linux v1.33.3 → v1.34.0 | |
| azure-monitor-metrics-cfg-reader 6.24.0-main | customer-net-probe master.250827.1 | kubernetes-cri-tools 1.32.0-ubuntu22.04u3 | metrics-server v0.7.2-10 → v0.8.0-4 | |
| azure-monitor-metrics-ksm v2.17.0 | envoy v1.35.6-master.251017.3 | nvidia-device-plugin 0.18.0-ubuntu22.04u2 | overlay-vpa v1.2.1-1 → v1.5.1-1 | |
| azure-monitor-metrics-linux 6.24.0-main | ingress-dispatcher v1.35.6-master.251017.3 | runc 1.3.3-ubuntu22.04u1 | coredns v1.12.1-7 → v1.13.1-2 | |
| azure-monitor-metrics-target-allocator | jwt-authenticator-egress master.250904.1 | Linux - AzureLinux 3.0 |
kube-egress-gateway-controller v0.0.21 → v0.1.3 | |
| azure-monitor-metrics-windows | kube-state-metrics v2.15.0-4 | azure-acr-credential-provider-pmc 1.34.1-1.azl3 | ||
| azure-npm-image v1.6.34 | kubeguard-guard v0.16.23 | containerd 2.0.0-14.azl3 | ||
| azure-npm-image-windows v1.5.5 | private-connect-balancer master.250731.2 | datacenter-gpu-manager-4-core 1:4.4.1-1 | ||
| azure-policy 1.15.1 | private-connect-router master.251105.2 | datacenter-gpu-manager-4-proprietary 1:4.4.1-1 | ||
| azure-policy-audit 1.15.1 | gpu-provisioner 0.3.7 (plugin) | dcgm-exporter 4.6.0-1.azl3 | ||
| azure-policy-webhook 1.15.1 | karpenter 1.6.5-aks (plugin) | kubectl 1.34.1-4.azl3 | ||
| certgen v0.1.9 | kms-controller master.250811.2 (plugin) | kubelet 1.34.1-4.azl3 | ||
| cilium-agent 1.14.10-1 | kms-operator master.250814.1 (plugin) | kubernetes-cri-tools 1.32.0-3.azl3 | ||
| cilium-envoy v1.31.5-250218 | kms-plugin-v2-plus master.251114.2 (plugin) | nvidia-container-toolkit 1.17.3 | ||
| cilium-operator-generic 1.14.10 | kube-egress-gateway-controller v0.1.3 | nvidia-device-plugin 0.18.0-2.azl3 | ||
| cloud-provider-node-manager-linux v1.34.0 | kubelet-serving-csr-approver v0.0.7 | Windows - Windows2022 |
||
| cloud-provider-node-manager-windows v1.34.0 | live-patching-controller v0.0.16 | containerd v2.0.4-azure.1 | ||
| ... | secure-tls-bootstrap-server v0.0.9 |

### Kubernetes 1.33

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes From Kubernetes 1.33.0 |
Notes |
|---|---|---|---|---|
| * aci-connector-linux 1.6.2 * addon-resizer v1.8.23-2 * ai-toolchain-operator 0.4.5 * aks-windows-gpu-device-plugin 0.0.19 * ama-logs-linux 3.1.26 * ama-logs-win win-3.1.26 * app-routing-operator 0.0.3 * azure-monitor-metrics-cfg-reader 6.16.0-main-04-15-2025-d78050c6-cfg * azure-monitor-metrics-ksm v2.15.0-4 * azure-monitor-metrics-linux 6.16.0-main-04-15-2025-d78050c6 * azure-monitor-metrics-target-allocator 6.16.0-main-04-15-2025-d78050c6-targetallocator * azure-monitor-metrics-windows 6.16.0-main-04-15-2025-d78050c6-win * azure-npm-image v1.5.45 * azure-npm-image-windows v1.5.5 * azure-policy 1.10.1 * azure-policy-webhook 1.10.0 * certgen v0.1.9 * cilium-agent 1.14.10-1 * cilium-envoy v1.31.5-250218 * cilium-operator-generic 1.14.10 * cloud-provider-node-manager-linux v1.33.0 * cloud-provider-node-manager-windows v1.33.0 * cluster-proportional-autoscaler v1.9.0-1 * container-networking-cilium-agent v1.16.6-250129 * container-networking-cilium-operator-generic v1.16.6-250129 * coredns v1.12.1-1 * cost-analysis-agent v0.0.23 * cost-analysis-opencost v1.111.0 * cost-analysis-prometheus v2.54.1 * cost-analysis-victoria-metrics v1.103.0 * extension-config-agent 1.23.3 * extension-manager 1.23.3 * fqdn-policy v1.16.6-250129 * gpu-provisioner 0.3.3 * health-probe-proxy v1.29.1 * hubble-relay v1.15.0 * image-cleaner v1.3.1 * ingress-appgw 1.8.1 * ip-masq-agent-v2 v0.1.15-2 * ipv6-hp-bpf v0.0.1 * keda v2.16.1 * keda-admission-webhooks v2.16.1 * keda-metrics-apiserver v2.16.1 * kube-egress-gateway-cni v0.0.20 * kube-egress-gateway-cni-ipam v0.0.20 * kube-egress-gateway-cnimanager v0.0.20 * kube-egress-gateway-daemon v0.0.20 * kube-egress-gateway-daemon-init v0.0.20 * metrics-server v0.7.2-6 * microsoft-defender-admission-controller 20250325.2 * microsoft-defender-low-level-collector 2.0.205 * microsoft-defender-low-level-init 1.3.81 * microsoft-defender-old-file-cleaner 1.0.214 * microsoft-defender-pod-collector 1.0.177 * microsoft-defender-security-publisher 1.0.211 * open-policy-agent-gatekeeper v3.18.2-1 * osm-bootstrap v1.2.9 * osm-controller v1.2.9 * osm-crds v1.2.9 * osm-healthcheck v1.2.9 * osm-init v1.2.9 * osm-injector v1.2.9 * osm-sidecar v1.32.2-hotfix.20241216 * overlay-vpa 1.2.1 * overlay-vpa-webhook-generation master.250430.1 * ratify-base v1.2.3 * retina-agent v0.0.31 * retina-agent-enterprise v0.1.9 * retina-agent-win v0.0.31 * retina-operator v0.1.9 * secrets-store-csi-driver v1.4.8 * secrets-store-csi-driver-windows v1.4.8 * secrets-store-driver-registrar-linux v2.11.1 * secrets-store-driver-registrar-windows v2.11.1 * secrets-store-livenessprobe-linux v2.13.1 * secrets-store-livenessprobe-windows v2.13.1 * secrets-store-provider-azure v1.6.2 * secrets-store-provider-azure-windows v1.6.2 * sgx-attestation 3.3.1 * sgx-plugin 1.0.0 * sgx-webhook 1.2.2 * tigera-operator v1.36.7 * windows-gmsa-webhook-image v0.12.1-2 * workload-identity-webhook v1.5.0 |
* addon-override-manager master.250116.1 * apiserver-network-proxy-server v0.30.3-hotfix.20240819 * app-routing-operator 0.2.5 * ccp-webhook master.250509.3 * cluster-autoscaler v1.32.1-aks * cost-analysis-scraper v0.0.23 * customer-net-probe master.250430.1 * envoy v1.31.5-master.241218.3 * ingress-dispatcher v1.31.5-master.250126.7 * kube-state-metrics v2.15.0-4 * gpu-provisioner 0.3.3 * karpenter 0.7.3-aks * kube-egress-gateway-controller v0.0.20 * kubelet-serving-csr-approver v0.0.7 * live-patching-controller v0.0.8 |
* Linux - Ubuntu 22.04 * containerd 1.7.27-ubuntu22.04u1 * kubernetes-cri-tools 1.32.0-ubuntu22.04u3 * runc 1.2.6-ubuntu22.04u1 * Linux - AzureLinux 3.0 * containerd 2.0.0-4.azl3 * nvidia-container-toolkit 1.17.3 * Windows - Windows2022 * containerd v1.7.20-azure.1 |
* coredns v1.11.3-7 → v1.12.1-1 * cloud-provider-node-manager-windows v1.32.5 → v1.33.0 * cloud-provider-node-manager-linux v1.32.5 → v1.33.0 |
N/A |

### Kubernetes 1.32

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.8.0 * Metrics-Server 0.6.3 * App routing operator v0.2.3 * KEDA 2.14.1 * Open Service Mesh v1.2.9 * Core DNS V1.9.4 * Overlay VPA 1.0.0 * Azure-Keyvault-SecretsProvider v1.4.5 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.3.1 * Azure Workload identity v1.3.0 * MDC Defender Low Level Collector 2.0.186 * open-policy-agent-gatekeeper v3.17.1 * Retina v0.0.17 |
* Cilium v1.17.0 * Cluster Autoscaler v1.30.6-aks * Tigera-Operator v1.34.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.23-ubuntu22.04u1 for Linux and v1.6.35+azure for Windows * Azure Linux 3.0 * Cgroups V2 * ContainerD 1.7.13-3.azl |
*
|

### Kubernetes 1.31

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.8.0 * Metrics-Server 0.6.3 * App routing operator v0.2.3 * KEDA 2.14.1 * Open Service Mesh v1.2.9 * Core DNS V1.9.4 * Overlay VPA 1.0.0 * Azure-Keyvault-SecretsProvider v1.4.5 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.3.1 * Azure Workload identity v1.3.0 * MDC Defender Low Level Collector 2.0.186 * open-policy-agent-gatekeeper v3.17.1 * Retina v0.0.17 |
* Cilium v1.16.6 * Cluster Autoscaler v1.30.6-aks * Tigera-Operator v1.30.11 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.23-ubuntu22.04u1 for Linux and v1.6.35+azure for Windows * Azure Linux 3.0 * Cgroups V2 * ContainerD 1.7.13-3.azl |
*
|

### Kubernetes 1.30

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.3.0 * App routing operator v0.2.3 * Metrics-Server 0.6.3 * KEDA 2.11.2 * Open Service Mesh 1.2.7 * Core DNS V1.9.4 * Overlay VPA 0.13.0 * Azure-Keyvault-SecretsProvider 1.4.1 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.2.3 * Azure Workload identity v1.2.0 * MDC Defender Security Publisher 1.0.68 * MDC Defender Old File Cleaner 1.3.68 * MDC Defender Pod Collector 1.0.78 * MDC Defender Low Level Collector 2.0.186 * Microsoft Entra Pod Identity 1.8.13.6 * GitOps 1.8.1 * CSI Secrets Store Driver 1.3.4-1 *
|
* Cilium v1.14.9 * CNI v1.4.43.1 (Default)/v1.5.11 (Azure CNI Overlay) * Cluster Autoscaler 1.27.3 * Tigera-Operator 1.30.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.5 for Linux and 1.7.1 for Windows * Azure Linux 2.0 * Cgroups V2 * ContainerD 1.6 |
* Tigera-Operator 1.30.7 | N/A |

### Kubernetes 1.29

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.3.0 * csi-provisioner v4.0.0 * App routing operator v0.2.1 * csi-attacher v4.5.0 * csi-snapshotter v6.3.3 * snapshot-controller v6.3.3 * Metrics-Server 0.6.3 * KEDA 2.11.2 * Open Service Mesh 1.2.7 * Core DNS V1.9.4 * Overlay VPA 0.13.0 * Azure-Keyvault-SecretsProvider 1.4.1 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.2.3 * Azure Workload identity v1.2.0 * MDC Defender Security Publisher 1.0.68 * MDC Defender Old File Cleaner 1.3.68 * MDC Defender Pod Collector 1.0.78 * MDC Defender Low Level Collector 2.0.186 * Microsoft Entra Pod Identity 1.8.13.6 * GitOps 1.8.1 * CSI Secrets Store Driver 1.3.4-1 * azurefile-csi-driver 1.29.3 |
* Cilium v1.14.9 * CNI v1.4.43.1 (Default)/v1.5.11 (Azure CNI Overlay) * Cluster Autoscaler 1.27.3 * Tigera-Operator 1.30.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.5 for Linux and 1.7.1 for Windows * Azure Linux 2.0 * Cgroups V2 * ContainerD 1.6 |
* Tigera-Operator 1.30.7 * csi-provisioner v4.0.0 * csi-attacher v4.5.0 * csi-snapshotter v6.3.3 * snapshot-controller v6.3.3 |
N/A |

## Alias minor version

Note

Alias minor version requires Azure CLI version 2.37 or above and API version 20220401 or above. Use `az upgrade`

to install the latest version of the CLI.

You can create an AKS cluster without specifying a patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. For example, if you create a cluster with ** 1.29** and

**is the latest GA would patch available, your cluster is created with**

`1.29.2`

**. If you want to upgrade your patch version in the same minor version, use**

`1.29.2`

[autoupgrade](auto-upgrade-cluster).

To see what patch you're on, run the `az aks show --resource-group myResourceGroup --name myAKSCluster`

command. The `currentKubernetesVersion`

property shows the whole Kubernetes version.

```
{
"apiServerAccessProfile": null,
"autoScalerProfile": null,
"autoUpgradeProfile": null,
"azurePortalFqdn": "myaksclust-myresourcegroup.portal.hcp.eastus.azmk8s.io",
"currentKubernetesVersion": "1.29.2",
}
```


## Kubernetes version support policy

AKS defines a generally available (GA) version as a version available in all regions and enabled in all SLO or SLA measurements. AKS supports three GA minor versions of Kubernetes:

AKS supports three GA minor versions:

- The latest GA version (N).
- The two previous minor versions (N-1 and N-2).
- Each supported minor version can support any number of patches at a given time. AKS reserves the right to deprecate patches if a critical CVE or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to version release notes and visit the
[AKS release status webpage](release-tracker).

- Each supported minor version can support any number of patches at a given time. AKS reserves the right to deprecate patches if a critical CVE or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to version release notes and visit the

AKS might also support preview versions, which are explicitly labeled and subject to [preview terms and conditions](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

AKS provides platform support only for one GA minor version of Kubernetes after the regular supported versions. The platform support window of Kubernetes versions on AKS is known as "N-3". For more information, see [platform support policy](#platform-support-policy).

Note

AKS uses safe deployment practices that involve gradual region deployment. This means it might take up to 10 business days for a new release or a new version to be available in all regions.

The supported window of Kubernetes minor versions on AKS is known as "N-2", where N refers to the latest release, meaning that two previous minor releases are also supported.

For example, on the day that AKS introduces version 1.29, support is provided for the following versions:

| New minor version | Supported Minor Version List |
|---|---|
| 1.29 | 1.29, 1.28, 1.27 |

When a new minor version is introduced, the oldest minor version is deprecated and removed. For example, let's say the current supported minor version list is:

```
1.29
1.28
1.27
```


When AKS releases 1.30, all the 1.27 versions go out of support 30 days later.

AKS might support any number of **patches** based on upstream community release availability for a given minor version. AKS reserves the right to deprecate any of these patches at any given time due to a CVE or potential bug concern. You're always encouraged to use the latest patch for a minor version.

## Platform support policy

Platform support policy is a reduced support plan for certain unsupported Kubernetes versions. During platform support, customers only receive support from Microsoft for AKS/Azure platform related issues. Any issues related to Kubernetes functionality and components aren't supported.

Platform support policy applies to clusters in an n-3 version (where n is the latest supported AKS GA minor version), before the cluster drops to n-4. For example, Kubernetes v1.26 is considered platform support when v1.29 is the latest GA version. If you're a running an n-2 version, the moment it becomes n-3 , the version also becomes end of official support, and you enter into the platform support policy.

AKS relies on the releases and patches from [Kubernetes](https://kubernetes.io/releases/), which is an Open Source project that only supports a sliding window of three minor versions. AKS can only guarantee [full support](#kubernetes-version-support-policy) while those versions are being serviced upstream. Since there's no more patches being produced upstream, AKS can either leave those versions unpatched or fork. Due to this limitation, platform support doesn't support anything from relying on Kubernetes upstream.

This table outlines support guidelines for Community Support compared to Platform support.

| Support category | Community Support (N-2) | Platform Support (N-3) |
|---|---|---|
| Upgrades from N-3 to a supported version | Supported | Supported |
| Platform (Azure) availability | Supported | Supported |
| Node pool scaling | Supported | Supported |
| VM availability | Supported | Supported |
| Storage, Networking related issues | Supported | Supported except for bug fixes and retired components |
| Start/stop | Supported | Supported |
| Rotate certificates | Supported | Supported |
| Infrastructure SLA | Supported | Supported |
| Control Plane SLA | Supported | Supported |
| Platform (AKS) SLA | Supported | Not supported |
| Kubernetes components (including Add-ons) | Supported | Not supported |
| Component updates | Supported | Not supported |
| Component hotfixes | Supported | Not supported |
| Applying bug fixes | Supported | Not supported |
| Applying security patches | Supported | Not supported |
| Kubernetes API support | Supported | Not supported |
| Node pool creation | Supported | Supported |
| Cluster creation | Supported | Not Supported |
| Node pool snapshot | Supported | Not supported |
| Node image upgrade | Supported | Supported |

Note

The table is subject to change and outlines common support scenarios. Any scenarios related to Kubernetes functionality and components aren't supported for N-3. For further support, see [Support and troubleshooting for AKS](aks-support-help).

### Supported `kubectl`

versions

You can use a `kubectl`

version that is one minor version older or newer than your kube-apiserver version, [Kubernetes support policy for kubectl](https://kubernetes.io/docs/setup/release/version-skew-policy/#kubectl).

For example, if your *kube-apiserver* is at *1.28*, then you can use versions *1.27* to *1.29* of `kubectl`

with that *kube-apiserver*.

To install or update `kubectl`

to the latest version, run:

```
az aks install-cli
```


## Long Term Support (LTS)

AKS offers one year of Community Support and one year of Long Term Support (LTS), including backported security fixes from the upstream community. Our upstream LTS working group contributes efforts back to the community to provide our customers with a longer support window.

For more information on LTS, see [Long term support for Azure Kubernetes Service (AKS)](long-term-support).

## Release and deprecation process

You can reference upcoming version releases and deprecations on the [AKS Kubernetes release calendar](#aks-kubernetes-release-calendar).

For new **minor** versions of Kubernetes:

- AKS announces new version release dates and old version deprecation in the
[AKS Release notes](https://aka.ms/aks/releasenotes)at least 30 days before removal. - AKS uses
[Azure Advisor](/en-us/azure/advisor/advisor-overview)to alert you if a new version could cause issues in your cluster because of deprecated APIs. Azure Advisor also alerts you if you're out of support - AKS publishes a
[service health notification](/en-us/azure/service-health/service-health-overview)available to all users with AKS and portal access and sends an email to the subscription administrators with the planned version removal dates.Note

To find out who is your subscription administrators or to change it, refer to

[manage Azure subscriptions](/en-us/azure/cost-management-billing/manage/add-change-subscription-administrator#assign-a-subscription-administrator). - You have
**30 days**from version removal to upgrade to a supported minor version release to continue receiving support.

For new **patch** versions of Kubernetes:

- Because of the urgent nature of patch versions, they can be introduced into the service as they become available. Once available, patches have a two month minimum lifecycle.
- In general, AKS doesn't broadly communicate the release of new patch versions. However, AKS constantly monitors and validates available CVE patches to support them in AKS in a timely manner. If a critical patch is found or user action is required, AKS notifies you to upgrade to the newly available patch.
- You have
**30 days**from a patch release's removal from AKS to upgrade into a supported patch and continue receiving support. However, you'll**no longer be able to create clusters or node pools once the version is deprecated/removed.**

### Supported versions policy exceptions

AKS reserves the right to add or remove new/existing versions with one or more critical production-impacting bugs or security issues without advance notice.

Specific patch releases might be skipped or rollout accelerated, depending on the severity of the bug or security issue.

## Azure portal and CLI versions

If you deploy an AKS cluster with Azure portal, Azure CLI, Azure PowerShell, the cluster defaults to the N-1 minor version and latest patch. For example, if AKS supports *1.29.2*, *1.29.1*, *1.28.7*, *1.28.6*, *1.27.11*, and *1.27.10*, the default version selected is *1.28.7*.

To find out what versions are currently available for your subscription and region, use the
[ az aks get-versions](/en-us/cli/azure/aks#az-aks-get-versions) command. The following example lists the available Kubernetes versions for the

*EastUS*region:

```
az aks get-versions --location eastus --output table
```


## FAQ

### How does Microsoft notify me of new Kubernetes versions?

The AKS team announces new Kubernetes version release dates in our documentation, on [GitHub](https://github.com/Azure/AKS/releases), and via email to subscription administrators with clusters nearing end of support. AKS also uses [Azure Advisor](/en-us/azure/advisor/advisor-overview) to alert you inside the Azure portal if you're out of support and inform you of deprecated APIs that can affect your application or development process.

### How often should I expect to upgrade Kubernetes versions to stay in support?

Starting with Kubernetes 1.19, the [open source community expanded support to one year](https://kubernetes.io/blog/2020/08/31/kubernetes-1-19-feature-one-year-support/). AKS commits to enabling patches and support matching the upstream commitments. For AKS clusters on 1.19 and greater, you can upgrade at a minimum of once a year to stay on a supported version.

**What happens when you upgrade a Kubernetes cluster with a minor version that isn't supported?**

If you're on the *n-3* version or older, it means you're outside of support and need to upgrade. If your upgrade from version n-3 to n-2 succeeds, you're back within our support policies. For example:

- If the oldest supported AKS minor version is
*1.27*and you're on*1.26*or older, you're outside of support. - If you successfully upgrade from
*1.26*to*1.27*or higher, you're back within our support policies.

Downgrades aren't supported.

### What does 'Outside of Support' mean?

'Outside of Support' means that:

- The version you're running is outside of the supported versions list.
- You'll be asked to upgrade the cluster to a supported version when requesting support, unless you're within the 30-day grace period after version deprecation.

Additionally, AKS doesn't make any runtime or other guarantees for clusters outside of the supported versions list.

### What happens when you scale a Kubernetes cluster with a minor version that isn't supported?

For minor versions not supported by AKS, scaling in or out should continue to work. Since there are no guarantees with quality of service, we recommend upgrading to bring your cluster back into support.

### Can you stay on a Kubernetes version forever?

If a cluster is out of support for more than three minor versions and carries security risks, Azure proactively contacts you. They advise you to upgrade your cluster. If you don't take further action, Azure reserves the right to automatically upgrade your cluster on your behalf.

### What happens if you scale a Kubernetes cluster with a minor version that isn't supported?

For minor versions not supported by AKS, scaling in or out should continue to work. Since there are no guarantees with quality of service, we recommend upgrading to bring your cluster back into support.

### What version does the control plane support if the node pool isn't in one of the supported AKS versions?

The control plane must be within a window of versions from all node pools. For details on upgrading the control plane or node pools, visit documentation on [upgrading node pools](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools).

### What is the allowed difference in versions between control plane and node pool?

The [version skew policy](https://kubernetes.io/releases/version-skew-policy/) now allows a difference of up to three versions between control plane and agent pools. AKS follows this skew version policy change starting from version 1.28 onwards.

### Can I skip multiple AKS versions during cluster upgrade?

If you upgrade a supported AKS cluster, Kubernetes minor versions can't be skipped. Kubernetes control planes [version skew policy](https://kubernetes.io/releases/version-skew-policy/) doesn't support minor version skipping. For example, upgrades between:

*1.28.x*->*1.29.x*: allowed.*1.27.x*->*1.28.x*: allowed.*1.27.x*->*1.29.x*: not allowed.

For control plane version upgrades, you can go up to three minor versions for community supported versions in sequential fashion.

To upgrade from *1.27.x* -> *1.29.x*:

- Upgrade from
*1.27.x*->*1.28.x*. - Upgrade from
*1.28.x*->*1.29.x*.

Note starting from 1.28 version onwards, agentpool versions can be up to three versions older to control plane versions per [version skew policy](https://kubernetes.io/releases/version-skew-policy/). If your version is much behind the minimum supported version, you might have to do more than one control plane upgrade operation to get to the minimum supported version. For example, if your current control plane version is *1.23.x* and you intend to upgrade to a minimum supported version of *1.27.x* as an example. You might have to upgrade sequentially four times from *1.23.x* in order to get to *1.27.x*. Also note that Agent pool versions can be upgraded to the control plane minor version. In the previous example you can upgrade agentpool version twice, once from *1.23.x* to *1.25.x*, when the control plane version is at *1.25.x*. And then from *1.25.x* to *1.27.x*, when control plane version is at *1.27.x*. When you upgrade in-place, like control plane and agent pool together the same rules applicable to control plane upgrade applies.

If performing an upgrade from an *unsupported version* the upgrade is done without any guarantee of functionality and is excluded from the service-level agreements and limited warranty. Clusters running *unsupported version* has the flexibility of decoupling control plane upgrades with node pool upgrades. However if your version is out of date, we recommend that you re-create the cluster.

### Can I create a new 1.xx.x cluster during the platform support window?

No, Creation of new clusters isn't possible during Platform Support period.

### I'm on a freshly deprecated version that is out of platform support, can I still add new node pools? Or should I upgrade?

Yes, you can add agent pools as long as they're compatible with the control plane version.

## Next steps

For information on how to upgrade your cluster, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-annual-channel -->

# Use Windows Server Annual Channel for Containers on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS supports [Windows Server Annual Channel for Containers](https://techcommunity.microsoft.com/t5/windows-server-news-and-best/windows-server-annual-channel-for-containers/ba-p/3866248) in public preview. Each channel version is released annually and is supported for *two years*. This channel is beneficial if you require increased innovation cycles and portability.

Windows Server Annual Channel versions are based on the Kubernetes version of your node pool. To upgrade from one Annual Channel version to the next, you can [upgrade to a Kubernetes version](upgrade-aks-cluster) that supports the next Annual Channel version.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Supported Annual Channel releases

AKS releases support for new releases of Windows Server Annual Channel for Containers in alignment with Kubernetes versions. For the latest updates, see the [AKS release notes](https://github.com/Azure/AKS/releases). The following table provides an *estimated* release schedule for upcoming Annual Channel releases:

| K8s version | Annual Channel (host) version | Container image supported | End of support date |
|---|---|---|---|
| 1.28 | 23H2 (preview only) | Windows Server 2022 | End of 1.33 support |
| 1.34 | 24H2 | Windows Server 2022 & Windows Server 2025 | End of 1.35 support |

## Windows Server Annual Channel vs. Long Term Servicing Channel Releases (LTSC)

AKS supports Long Term Servicing Channel Releases (LTSC), including Windows Server 2025, Windows Server 2022, and Windows Server 2019. These come from a different release channel than Windows Server Annual Channel for Containers. To view our current recommendations, see the [Windows best practices documentation](windows-best-practices).

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes][aks-release-notes]. To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

The following table compares Windows Server Annual Channel and Long Term Servicing Channel releases:

| Channel | Support | Upgrades |
|---|---|---|
| Long Term Servicing Channel (LTSC) | LTSC channels are released every three years and are supported for five years. This channel is recommended for customers using Long Term Support. | To upgrade from one release to the next, you need to migrate your node pools to a new OS SKU option and rebuild your container images with the new OS version. |
| Windows Server Annual Channel for Containers | Annual Channel releases occur annually and are supported for two years. | To upgrade to the latest release, you can upgrade the Kubernetes version of your node pool. |

## Before you begin

- You need the Azure CLI version 2.56.0 or later installed and configured to set
`os-sku`

to`WindowsAnnual`

with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- Windows Server Annual Channel doesn't support Azure Network Policy Manager.

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `AKSWindowsAnnualPreview`

feature flag

Register the

`AKSWindowsAnnualPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSWindowsAnnualPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AKSWindowsAnnualPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Use Windows Server Annual Channel for Containers on AKS

To use Windows Server Annual Channel on AKS, specify the following parameters:

`os-type`

set to`Windows`

`os-sku`

set to`WindowsAnnual`


Windows Server Annual Channel versions are based on the Kubernetes version of your node pool. To check which release you'll get based on the Kubernetes version of your node pool, see the [supported Annual Channel releases](#supported-annual-channel-releases).

### Create a new Windows Server Annual Channel node pool

Create a Windows Server Annual Channel node pool using the

command. The following example creates a Windows Server Annual Channel node pool with the 23H2 release:`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --os-sku WindowsAnnual \ --kubernetes-version 1.29 --name $NODE_POOL_NAME \ --node-count 1`

Note

If you don't specify the Kubernetes version during node pool creation, AKS uses the same Kubernetes version as your cluster.


### Verify Windows Server Annual Channel node pool creation

Verify Windows Server Annual Channel node pool creation by checking the OS SKU of your node pool using

`kubectl describe node`

command.`kubectl describe node $NODE_POOL_NAME`

If you successfully created a Windows Server Annual Channel node pool, you should see the following output:

`Name: npwin Roles: agent Labels: agentpool=npwin ... kubernetes.azure.com/os=windows ... kubernetes.azure.com/node-image-version=AKSWindows-23H2-gen2 ... kubernetes.azure.com/os-sku=WindowsAnnual`


### Upgrade an existing node pool to Windows Server Annual Channel

You can upgrade an existing node pool from an LTSC release to Windows Server Annual Channel by following the guidance in [Upgrade the OS version for your Azure Kubernetes Service (AKS) Windows workloads](upgrade-windows-os).

To upgrade from one Annual Channel version to the next, you can [upgrade to a Kubernetes version](upgrade-aks-cluster) that supports the next Annual Channel version.

## Next steps

To learn more about Windows Containers on AKS, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/openfaas -->

# Use OpenFaaS on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[OpenFaaS](https://www.openfaas.com/) is a framework that uses containers to build serverless functions. As an open source project, it has gained large-scale adoption within the community. This document details installing and using OpenFaas on an Azure Kubernetes Service (AKS) cluster.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](concepts-clusters-workloads). - You need an active Azure subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - You need an AKS cluster. If you don't have an existing cluster, you can create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - You need to install the OpenFaaS CLI. For installation options, see the
[OpenFaaS CLI documentation](https://github.com/openfaas/faas-cli).

## Add the OpenFaaS helm chart repo

Navigate to

[Azure Cloud Shell](https://shell.azure.com).Add the OpenFaaS helm chart repo and update to the latest version using the following

`helm`

commands.`helm repo add openfaas https://openfaas.github.io/faas-netes/ helm repo update`


## Deploy OpenFaaS

As a good practice, OpenFaaS and OpenFaaS functions should be stored in their own Kubernetes namespace.

Create a namespace for the OpenFaaS system and functions using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/openfaas/faas-netes/master/namespaces.yml`

Generate a password for the OpenFaaS UI Portal and REST API using the following commands. The helm chart uses this password to enable basic authentication on the OpenFaaS Gateway, which is exposed to the Internet through a cloud LoadBalancer.

`# generate a random password PASSWORD=$(head -c 12 /dev/urandom | shasum| cut -d' ' -f1) kubectl -n openfaas create secret generic basic-auth \ --from-literal=basic-auth-user=admin \ --from-literal=basic-auth-password="$PASSWORD"`

Important

Using a username and password for authentication is an insecure pattern. If you have an OpenFaaS enterprise license, we recommend using

[Identity and Access Management (IAM) for OpenFaaS](https://www.openfaas.com/blog/walkthrough-iam-for-openfaas/)instead.Get the value for your password using the following

`echo`

command.`echo $PASSWORD`

Deploy OpenFaaS into your AKS cluster using the

`helm upgrade`

command.`helm upgrade openfaas --install openfaas/openfaas \ --namespace openfaas \ --set basic_auth=true \ --set functionNamespace=openfaas-fn \ --set serviceType=LoadBalancer`

Your output should look similar to the following condensed example output:

`NAME: openfaas LAST DEPLOYED: Tue Aug 29 08:26:11 2023 NAMESPACE: openfaas STATUS: deployed ... NOTES: To verify that openfaas has started, run: kubectl --namespace=openfaas get deployments -l "release=openfaas, app=openfaas" ...`

A public IP address is created for accessing the OpenFaaS gateway. Get the IP address using the

command.`kubectl get service`

`kubectl get service -l component=gateway --namespace openfaas`

Your output should look similar to the following example output:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE gateway ClusterIP 10.0.156.194 <none> 8080/TCP 7m gateway-external LoadBalancer 10.0.28.18 52.186.64.52 8080:30800/TCP 7m`

Test the OpenFaaS system by browsing to the external IP address on port 8080,

`http://52.186.64.52:8080`

in this example, where you're prompted to log in. The default user is`admin`

and your password can be retrieved using`echo $PASSWORD`

.Set

`$OPENFAAS_URL`

to the URL of the external IP address on port 8080 and log in with the Azure CLI using the following commands.`export OPENFAAS_URL=http://52.186.64.52:8080 echo -n $PASSWORD | ./faas-cli login -g $OPENFAAS_URL -u admin --password-stdin`


## Create first function

Navigate to the OpenFaaS system using your OpenFaaS URL.

Create a function using the OpenFaas portal by selecting

**Deploy A New Function**and search for**Figlet**.Select the

**Figlet**function, and then select**Deploy**.Invoke the function using the following

`curl`

command. Make sure you replace the IP address in the following example with your OpenFaaS gateway address.`curl -X POST http://52.186.64.52:8080/function/figlet -d "Hello Azure"`

Your output should look similar to the following example output:

`_ _ _ _ _ | | | | ___| | | ___ / \ _____ _ _ __ ___ | |_| |/ _ \ | |/ _ \ / _ \ |_ / | | | '__/ _ \ | _ | __/ | | (_) | / ___ \ / /| |_| | | | __/ |_| |_|\___|_|_|\___/ /_/ \_\/___|\__,_|_| \___|`


## Create second function

### Configure your Azure Cosmos DB instance

Navigate to

[Azure Cloud Shell](https://shell.azure.com).Create a new resource group for the Azure Cosmos DB instance using the

command.`az group create`

`az group create --name serverless-backing --location eastus`

Deploy an Azure Cosmos DB instance of kind

`MongoDB`

using thecommand. Replace`az cosmosdb create`

`openfaas-cosmos`

with your own unique instance name.`az cosmosdb create --resource-group serverless-backing --name openfaas-cosmos --kind MongoDB`

Get the Azure Cosmos DB database connection string and store it in a variable using the

command. Make sure you replace the value for the`az cosmosdb keys list`

`--resource-group`

argument with the name of your resource group, and the`--name`

argument with the name of your Azure Cosmos DB instance.`COSMOS=$(az cosmosdb keys list \ --type connection-strings \ --resource-group serverless-backing \ --name openfaas-cosmos \ --output tsv)`

Populate the Azure Cosmos DB with test data by creating a file named

`plans.json`

and copying in the following json.`{ "name" : "two_person", "friendlyName" : "Two Person Plan", "portionSize" : "1-2 Person", "mealsPerWeek" : "3 Unique meals per week", "price" : 72, "description" : "Our basic plan, delivering 3 meals per week, which will feed 1-2 people.", "__v" : 0 }`


### Create the function

Install the MongoDB tools. The following example command installs these tools using brew. For more installation options, see the

[MongoDB documentation](https://docs.mongodb.com/manual/installation/).`brew install mongodb`

Load the Azure Cosmos DB instance with data using the

*mongoimport*tool.`mongoimport --uri=$COSMOS -c plans < plans.json`

Your output should look similar to the following example output:

`2018-02-19T14:42:14.313+0000 connected to: localhost 2018-02-19T14:42:14.918+0000 imported 1 document`

Create the function using the

`faas-cli deploy`

command. Make sure you update the value of the`-g`

argument with your OpenFaaS gateway address.`faas-cli deploy -g http://52.186.64.52:8080 --image=shanepeckham/openfaascosmos --name=cosmos-query --env=NODE_ENV=$COSMOS`

Once deployed, your output should look similar to the following example output:

`Deployed. 202 Accepted. URL: http://52.186.64.52:8080/function/cosmos-query`

Test the function using the following

`curl`

command. Make sure you update the IP address with the OpenFaaS gateway address.`curl -s http://52.186.64.52:8080/function/cosmos-query`

Your output should look similar to the following example output:

`[{"ID":"","Name":"two_person","FriendlyName":"","PortionSize":"","MealsPerWeek":"","Price":72,"Description":"Our basic plan, delivering 3 meals per week, which will feed 1-2 people."}]`

Note

You can also test the function within the OpenFaaS UI:


## Next steps

Continue to learn with the [OpenFaaS workshop](https://github.com/openfaas/workshop), which includes a set of hands-on labs that cover topics such as how to create your own GitHub bot, consuming secrets, viewing metrics, and autoscaling.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-ad-integration-cli -->

# Integrate Microsoft Entra ID with Azure Kubernetes Service (AKS) using the Azure CLI (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Warning

The feature described in this document, Microsoft Entra Integration (legacy) was **deprecated on June 1st, 2023**. At this time, no new clusters can be created with Microsoft Entra Integration (legacy).

AKS has a new improved [AKS-managed Microsoft Entra ID](managed-azure-ad) experience that doesn't require you to manage server or client applications. If you want to migrate follow the instructions [here](managed-azure-ad#migrate-a-legacy-azure-ad-cluster-to-integration).

Azure Kubernetes Service (AKS) can be configured to use Microsoft Entra ID for user authentication. In this configuration, you can log into an AKS cluster using a Microsoft Entra authentication token. Cluster operators can also configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership.

This article shows you how to create the required Microsoft Entra components, then deploy a Microsoft Entra ID-enabled cluster and create a basic Kubernetes role in the AKS cluster.

## Limitations

- Microsoft Entra ID can only be enabled on Kubernetes RBAC-enabled cluster.
- Microsoft Entra legacy integration can only be enabled during cluster creation.

## Before you begin

You need the Azure CLI version 2.0.61 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Go to [https://shell.azure.com](https://shell.azure.com) to open Cloud Shell in your browser.

For consistency and to help run the commands in this article, create a variable for your desired AKS cluster name. The following example uses the name *myakscluster*:

```
aksname="myakscluster"
```


## Microsoft Entra authentication overview

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc).

From inside of the Kubernetes cluster, Webhook Token Authentication is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster. For more information on Webhook token authentication, see the [webhook authentication documentation](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication).

Note

When configuring Microsoft Entra ID for AKS authentication, two Microsoft Entra applications are configured. This operation must be completed by an Azure tenant administrator.

## Create Microsoft Entra server component

To integrate with AKS, you create and use a Microsoft Entra application that acts as an endpoint for the identity requests. The first Microsoft Entra application you need gets Microsoft Entra group membership for a user.

Create the server application component using the [az ad app create](/en-us/cli/azure/ad/app#az-ad-app-create) command, then update the group membership claims using the [az ad app update](/en-us/cli/azure/ad/app#az-ad-app-update) command. The following example uses the *aksname* variable defined in the [Before you begin](#before-you-begin) section, and creates a variable

```
# Create the Azure AD application
serverApplicationId=$(az ad app create \
--display-name "${aksname}Server" \
--identifier-uris "https://${aksname}Server" \
--query appId -o tsv)
# Update the application group membership claims
az ad app update --id $serverApplicationId --set groupMembershipClaims=All
```


Now create a service principal for the server app using the [az ad sp create](/en-us/cli/azure/ad/sp#az-ad-sp-create) command. This service principal is used to authenticate itself within the Azure platform. Then, get the service principal secret using the [az ad sp credential reset](/en-us/cli/azure/ad/sp/credential#az-ad-sp-credential-reset) command and assign to the variable named *serverApplicationSecret* for use in one of the following steps:

```
# Create a service principal for the Azure AD application
az ad sp create --id $serverApplicationId
# Get the service principal secret
serverApplicationSecret=$(az ad sp credential reset \
--name $serverApplicationId \
--credential-description "AKSPassword" \
--query password -o tsv)
```


The Microsoft Entra service principal needs permissions to perform the following actions:

- Read directory data
- Sign in and read user profile

Assign these permissions using the [az ad app permission add](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-add) command:

```
az ad app permission add \
--id $serverApplicationId \
--api 00000003-0000-0000-c000-000000000000 \
--api-permissions e1fe6dd8-ba31-4d61-89e7-88639da4683d=Scope 06da0dbc-49e2-44d2-8312-53f166ab848a=Scope 7ab1d382-f21e-4acd-a863-ba3e13f7da61=Role
```


Finally, grant the permissions assigned in the previous step for the server application using the [az ad app permission grant](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-grant) command. This step fails if the current account is not a tenant admin. You also need to add permissions for Microsoft Entra application to request information that may otherwise require administrative consent using the [az ad app permission admin-consent](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-admin-consent):

```
az ad app permission grant --id $serverApplicationId --api 00000003-0000-0000-c000-000000000000
az ad app permission admin-consent --id $serverApplicationId
```


## Create Microsoft Entra client component

The second Microsoft Entra application is used when a user logs to the AKS cluster with the Kubernetes CLI (`kubectl`

). This client application takes the authentication request from the user and verifies their credentials and permissions. Create the Microsoft Entra app for the client component using the [az ad app create](/en-us/cli/azure/ad/app#az-ad-app-create) command:

```
clientApplicationId=$(az ad app create \
--display-name "${aksname}Client" \
--native-app \
--reply-urls "https://${aksname}Client" \
--query appId -o tsv)
```


Create a service principal for the client application using the [az ad sp create](/en-us/cli/azure/ad/sp#az-ad-sp-create) command:

```
az ad sp create --id $clientApplicationId
```


Get the oAuth2 ID for the server app to allow the authentication flow between the two app components using the [az ad app show](/en-us/cli/azure/ad/app#az-ad-app-show) command. This oAuth2 ID is used in the next step.

```
oAuthPermissionId=$(az ad app show --id $serverApplicationId --query "oauth2Permissions[0].id" -o tsv)
```


Add the permissions for the client application and server application components to use the oAuth2 communication flow using the [az ad app permission add](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-add) command. Then, grant permissions for the client application to communication with the server application using the [az ad app permission grant](/en-us/cli/azure/ad/app/permission#az-ad-app-permission-grant) command:

```
az ad app permission add --id $clientApplicationId --api $serverApplicationId --api-permissions ${oAuthPermissionId}=Scope
az ad app permission grant --id $clientApplicationId --api $serverApplicationId
```


## Deploy the cluster

With the two Microsoft Entra applications created, now create the AKS cluster itself. First, create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command. The following example creates the resource group in the *EastUS* region:

Create a resource group for the cluster:

```
az group create --name myResourceGroup --location EastUS
```


Get the tenant ID of your Azure subscription using the [az account show](/en-us/cli/azure/account#az-account-show) command. Then, create the AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The command to create the AKS cluster provides the server and client application IDs, the server application service principal secret, and your tenant ID:

```
tenantId=$(az account show --query tenantId -o tsv)
az aks create \
--resource-group myResourceGroup \
--name $aksname \
--node-count 1 \
--generate-ssh-keys \
--aad-server-app-id $serverApplicationId \
--aad-server-app-secret $serverApplicationSecret \
--aad-client-app-id $clientApplicationId \
--aad-tenant-id $tenantId
```


Finally, get the cluster admin credentials using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. In one of the following steps, you get the regular *user* cluster credentials to see the Microsoft Entra authentication flow in action.

```
az aks get-credentials --resource-group myResourceGroup --name $aksname --admin
```


## Create Kubernetes RBAC binding

Before a Microsoft Entra account can be used with the AKS cluster, a role binding or cluster role binding needs to be created. *Roles* define the permissions to grant, and *bindings* apply them to desired users. These assignments can be applied to a given namespace, or across the entire cluster. For more information, see [Using Kubernetes RBAC authorization](concepts-identity#kubernetes-rbac).

Get the user principal name (UPN) for the user currently logged in using the [az ad signed-in-user show](/en-us/cli/azure/ad/signed-in-user#az-ad-signed-in-user-show) command. This user account is enabled for Microsoft Entra integration in the next step.

```
az ad signed-in-user show --query userPrincipalName -o tsv
```


Important

If the user you grant the Kubernetes RBAC binding for is in the same Microsoft Entra tenant, assign permissions based on the *userPrincipalName*. If the user is in a different Microsoft Entra tenant, query for and use the *objectId* property instead.

Create a YAML manifest named `basic-azure-ad-binding.yaml`

and paste the following contents. On the last line, replace *userPrincipalName_or_objectId* with the UPN or object ID output from the previous command:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
name: contoso-cluster-admins
roleRef:
apiGroup: rbac.authorization.k8s.io
kind: ClusterRole
name: cluster-admin
subjects:
- apiGroup: rbac.authorization.k8s.io
kind: User
name: userPrincipalName_or_objectId
```


Create the ClusterRoleBinding using the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify the filename of your YAML manifest:

```
kubectl apply -f basic-azure-ad-binding.yaml
```


## Access cluster with Microsoft Entra ID

Now let's test the integration of Microsoft Entra authentication for the AKS cluster. Set the `kubectl`

config context to use regular user credentials. This context passes all authentication requests back through Microsoft Entra ID.

```
az aks get-credentials --resource-group myResourceGroup --name $aksname --overwrite-existing
```


Now use the [kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to view pods across all namespaces:

```
kubectl get pods --all-namespaces
```


You receive a sign in prompt to authenticate using Microsoft Entra credentials using a web browser. After you've successfully authenticated, the `kubectl`

command displays the pods in the AKS cluster, as shown in the following example output:

```
kubectl get pods --all-namespaces
```


```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code BYMK7UXVD to authenticate.
NAMESPACE NAME READY STATUS RESTARTS AGE
kube-system coredns-754f947b4-2v75r 1/1 Running 0 23h
kube-system coredns-754f947b4-tghwh 1/1 Running 0 23h
kube-system coredns-autoscaler-6fcdb7d64-4wkvp 1/1 Running 0 23h
kube-system heapster-5fb7488d97-t5wzk 2/2 Running 0 23h
kube-system kube-proxy-2nd5m 1/1 Running 0 23h
kube-system kube-svc-redirect-swp9r 2/2 Running 0 23h
kube-system kubernetes-dashboard-847bb4ddc6-trt7m 1/1 Running 0 23h
kube-system metrics-server-7b97f9cd9-btxzz 1/1 Running 0 23h
kube-system tunnelfront-6ff887cffb-xkfmq 1/1 Running 0 23h
```


The authentication token received for `kubectl`

is cached. You are only reprompted to sign in when the token has expired or the Kubernetes config file is re-created.

If you see an authorization error message after you've successfully signed in using a web browser as in the following example output, check the following possible issues:

```
error: You must be logged in to the server (Unauthorized)
```


- You defined the appropriate object ID or UPN, depending on if the user account is in the same Microsoft Entra tenant or not.
- The user is not a member of more than 200 groups.
- Secret defined in the application registration for server matches the value configured using
`--aad-server-app-secret`

- Be sure that only one version of kubectl is installed on your machine at a time. Conflicting versions can cause issues during authorization. To install the latest version, use
[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli).

## Frequently asked questions about migration from Microsoft Entra Integration to AKS-managed Microsoft Entra ID

**1. What is the plan for migration?**

Microsoft Entra Integration (legacy) will be deprecated on 1st June 2023. After this date, you won't be able to create new clusters with Microsoft Entra ID (legacy). We'll migrate all Microsoft Entra Integration (legacy) AKS clusters to AKS-managed Microsoft Entra ID automatically starting from 1st August 2023. We send notification emails to impacted subscription admins biweekly to remind them of migration.

**2. What will happen if I don't take any action?**

Your Microsoft Entra Integration (legacy) AKS clusters will continue working after 1st June 2023. We'll automatically migrate your clusters to AKS-managed Microsoft Entra ID starting from 1st August 2023. You may experience API server downtime during the migration.

The kubeconfig content changes after the migration. You need to merge the new credentials into the kubeconfig file using the `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

.

We recommend updating your AKS cluster to [AKS-managed Microsoft Entra ID](managed-azure-ad#migrate-a-legacy-azure-ad-cluster-to-integration) manually before 1st August. This way you can manage the downtime during non-business hours when it's more convenient.

**3. Why do I still receive the notification email after manual migration?**

It takes several days for the email to send. If your cluster wasn't migrated before we initiate the email-sending process, you may still receive a notification.

**4. How can I check whether my cluster my cluster is migrated to AKS-managed Microsoft Entra ID?**

Confirm your AKS cluster is migrated to the AKS-managed Microsoft Entra ID using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command.

```
az aks show -g <RGName> -n <ClusterName> --query "aadProfile"
```


If your cluster is using the AKS-managed Microsoft Entra ID, the output shows `managed`

is `true`

. For example:

```
{
"adminGroupObjectIDs": [
"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
],
"adminUsers": null,
"clientAppId": null,
"enableAzureRbac": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
}
```


## Next steps

For the complete script that contains the commands shown in this article, see the [Microsoft Entra integration script in the AKS samples repo][complete-script].

To use Microsoft Entra users and groups to control access to cluster resources, see [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

For more information about how to secure Kubernetes clusters, see [Access and identity options for AKS)](concepts-identity#kubernetes-rbac).

For best practices on identity and resource control, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux-os-guard -->

# Azure Linux with OS Guard (preview) for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Azure Linux with OS Guard (preview) on Azure Kubernetes Service (AKS), including key features, region availability, and resources to get started.

## What is Azure Linux with OS Guard?

Azure Linux with OS Guard is a hardened, immutable variant of Azure Linux. It provides strong runtime integrity, tamper resistance, and enterprise-grade security for container hosts on AKS. OS Guard is built on Azure Linux and adds kernel and runtime features that enforce code integrity, protect the root file system from unauthorized changes, and apply mandatory access controls.

You can deploy Azure Linux with OS Guard node pools in a new cluster, add Azure Linux with OS Guard node pools to your existing Azure Linux or Ubuntu clusters, or migrate your Azure Linux or Ubuntu nodes to Azure Linux with OS Guard nodes.

To learn more about Azure Linux with OS Guard, see the [Azure Linux with OS Guard documentation](/en-us/azure/azure-linux/intro-azure-linux-os-guard).

## Why use Azure Linux with OS Guard on AKS?

Azure Linux with OS Guard on AKS builds on the benefits of [Azure Linux](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-key-benefits) by adding enhanced security features that help protect your container workloads from advanced threats. OS Guard provides:

**Immutability**: The`/usr`

directory is mounted as a read-only volume protected by dm-verity, preventing execution of tampered or untrusted code.**Code integrity**: OS Guard integrates the[Integrity Policy Enforcement (IPE) Linux Security Module](https://docs.kernel.org/next/admin-guide/LSM/ipe.html)to ensure that only binaries from trusted, signed volumes are allowed to execute. (**IPE is running in audit mode during Public Preview**.)**Mandatory access controls**: OS Guard integrates SELinux to limit which processes can access sensitive resources in the system. (**SELinux is operating in permissive mode during Public Preview**.)**Integration with Azure security features**: Native support for[Trusted Launch](/en-us/azure/aks/use-trusted-launch)and Secure Boot provides measured boot protections and attestation.**Verified container layers**: Container images and layers are validated using signed dm-verity hashes. This ensures that only verified layers are used at runtime, reducing the risk of container escape or tampering.**Sovereign Supply Chain Security**: OS Guard inherits Azure Linux’s secure build pipelines, signed Unified Kernel Images (UKIs) and Software Bill of Materials (SBOMs).

Learn more about the [key features of Azure Linux with OS Guard](/en-us/azure/azure-linux/intro-azure-linux-os-guard).

## Regional availability

Azure Linux with OS Guard is available for use in the same [regions](/en-us/azure/aks/quotas-skus-regions) as AKS.

## Get started with Azure Linux with OS Guard on AKS

Get started with Azure Linux with OS Guard on AKS using the following resources:

[Creating a cluster with Azure Linux with OS Guard](/en-us/azure/azure-linux/quickstart-os-guard-azure-cli)[How to upgrade Azure Linux with OS Guard clusters](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-upgrade)[Add an Azure Linux with OS Guard node pool to your existing cluster](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-add-node-pool)[Migrate to Azure Linux with OS Guard](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-migration)[Enable telemetry and monitoring on an Azure Linux with OS Guard cluster](/en-us/azure/azure-linux/tutorial-azure-linux-os-guard-telemetry-monitor)

## Next steps

To learn more about Azure Linux with OS Guard, see the [Azure Linux with OS Guard documentation](/en-us/azure/azure-linux/intro-azure-linux-os-guard).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-windows-hpc -->

# Use Windows HostProcess containers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

HostProcess / Privileged containers extend the Windows container model to enable a wider range of Kubernetes cluster management scenarios. HostProcess containers run directly on the host and maintain behavior and access similar to that of a regular process. HostProcess containers allow users to package and distribute management operations and functionalities that require host access while retaining versioning and deployment methods provided by containers.

A privileged DaemonSet can carry out changes or monitor a Linux host on Kubernetes but not Windows hosts. HostProcess containers are the Windows equivalent of host elevation.

## Limitations

- HostProcess containers require Kubernetes 1.23 or greater.
- HostProcess containers require
`containerd`

1.6 or higher container runtime. - HostProcess pods can only contain HostProcess containers due to a limitation on the Windows operating system. Non-privileged Windows containers can't share a vNIC with the host IP namespace.
- HostProcess containers run as a process on the host. The only isolation those containers have from the host is the resource constraints imposed on the HostProcess user account.
- Filesystem isolation and Hyper-V isolation aren't supported for HostProcess containers.
- Volume mounts are supported and are mounted under the container volume. See Volume Mounts.
- A limited set of host user accounts are available for Host Process containers by default. See Choosing a User Account.
- Resource limits such as disk, memory, and cpu count, work the same way as fashion as processes on the host.
- Named pipe mounts and Unix domain sockets aren't directly supported, but can be accessed on their host path, for example
`\\.\pipe\*`

.

## Run a HostProcess workload

To use HostProcess features with your deployment, set *hostProcess: true* and *hostNetwork: true*:

```
spec:
...
securityContext:
windowsOptions:
hostProcess: true
...
hostNetwork: true
containers:
...
```


To run an example workload that uses HostProcess features on an existing AKS cluster with Windows nodes, create `hostprocess.yaml`

with the following contents:

```
apiVersion: apps/v1
kind: DaemonSet
metadata:
name: privileged-daemonset
namespace: kube-system
labels:
app: privileged-daemonset
spec:
selector:
matchLabels:
app: privileged-daemonset
template:
metadata:
labels:
app: privileged-daemonset
spec:
nodeSelector:
kubernetes.io/os: windows
securityContext:
windowsOptions:
hostProcess: true
runAsUserName: "NT AUTHORITY\\SYSTEM"
hostNetwork: true
containers:
- name: powershell
image: mcr.microsoft.com/windows/nanoserver:ltsc2019 # or nanoserver:ltsc2022
command:
- powershell.exe
- -Command
- Start-Sleep -Seconds 2147483
terminationGracePeriodSeconds: 0
```


Use `kubectl`

to run the example workload:

```
kubectl apply -f hostprocess.yaml
```


You should see the following output:

```
$ kubectl apply -f hostprocess.yaml
daemonset.apps/privileged-daemonset created
```


Verify that your workload uses the features of HostProcess containers by viewing the pod's logs.

Use `kubectl`

to find the name of the pod in the `kube-system`

namespace.

```
$ kubectl get pods --namespace kube-system
NAME READY STATUS RESTARTS AGE
...
privileged-daemonset-12345 1/1 Running 0 2m13s
```


Use `kubectl log`

to view the logs of the pod and verify the pod has administrator rights:

```
$ kubectl logs privileged-daemonset-12345 --namespace kube-system
InvalidOperation: Unable to find type [Security.Principal.WindowsPrincipal].
Process has admin rights:
```


## Next steps

For more information on HostProcess containers and Microsoft's contribution to Kubernetes upstream, see the [Alpha in v1.22: Windows HostProcess Containers](https://kubernetes.io/blog/2021/08/16/windows-hostprocess-containers/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-pod-security -->

# Best practices for pod security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), the security of your pods is a key consideration. Your applications should be designed for the principle of least number of privileges required. Keeping private data secure is top of mind for customers. You don't want credentials like database connection strings, keys, or secrets and certificates exposed to the outside world where an attacker could take advantage of those secrets for malicious purposes. Don't add them to your code or embed them in your container images. This approach would create a risk for exposure and limit the ability to rotate those credentials as the container images will need to be rebuilt.

This best practices article focuses on how to secure pods in AKS. You learn how to:

- Use pod security context to limit access to processes and services or privilege escalation
- Authenticate with other Azure resources using Microsoft Entra Workload ID
- Request and retrieve credentials from a digital vault such as Azure Key Vault

You can also read the best practices for [cluster security](operator-best-practices-cluster-security) and for [container image management](operator-best-practices-container-image-management).

## Secure pod access to resources

**Best practice guidance** - To run as a different user or group and limit access to the underlying node processes and services, define pod security context settings. Assign the least number of privileges required.

For your applications to run correctly, pods should run as a defined user or group and not as *root*. The `securityContext`

for a pod or container lets you define settings such as *runAsUser* or *fsGroup* to assume the appropriate permissions. Only assign the required user or group permissions, and don't use the security context as a means to assume additional permissions. The *runAsUser*, privilege escalation, and other Linux capabilities settings are only available on Linux nodes and pods.

When you run as a non-root user, containers cannot bind to the privileged ports under 1024. In this scenario, Kubernetes Services can be used to disguise the fact that an app is running on a particular port.

A pod security context can also define additional capabilities or permissions for accessing processes and services. The following common security context definitions can be set:

**allowPrivilegeEscalation**defines if the pod can assume*root*privileges. Design your applications so this setting is always set to*false*.**Linux capabilities**let the pod access underlying node processes. Take care with assigning these capabilities. Assign the least number of privileges needed. For more information, see[Linux capabilities](http://man7.org/linux/man-pages/man7/capabilities.7.html).**SELinux labels**is a Linux kernel security module that lets you define access policies for services, processes, and filesystem access. Again, assign the least number of privileges needed. For more information, see[SELinux options in Kubernetes](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#selinuxoptions-v1-core)**hostUsers: false**the pod runs using a user-namespace, a Linux kernel feature. This significatly improves the host isolation and limits the lateral movement in case of container breakouts. These improvements are significant whether the container is running as root or not. For more information, see[user-namespaces](secure-container-access#user-namespaces).

The following example pod YAML manifest sets security context settings to define:

- Pod runs as user ID
*1000*and part of group ID*2000* - Can't escalate privileges to use
`root`

- Allows Linux capabilities to access network interfaces and the host's real-time (hardware) clock

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
fsGroup: 2000
containers:
- name: security-context-demo
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
securityContext:
runAsUser: 1000
allowPrivilegeEscalation: false
capabilities:
add: ["NET_ADMIN", "SYS_TIME"]
```


Work with your cluster operator to determine which security context settings you need. Design your applications to minimize other permissions and access the pod requires. There are other security features to limit access using AppArmor, seccomp (secure computing), and user-namespaces that can be implemented by cluster operators.

For more information, see [Secure container access to resources](operator-best-practices-cluster-security#secure-container-access-to-resources).

## Limit credential exposure

**Best practice guidance** - Don't define credentials in your application code. Use managed identities for Azure resources to let your pod request access to other resources. A digital vault, such as Azure Key Vault, should also be used to store and retrieve digital keys and credentials. Pod-managed identities are intended for use with Linux pods and container images only.

To limit the risk of credentials being exposed in your application code, avoid the use of fixed or shared credentials. Credentials or keys shouldn't be included directly in your code. If these credentials are exposed, the application needs to be updated and redeployed. A better approach is to give pods their own identity and way to authenticate themselves, or automatically retrieve credentials from a digital vault.

#### Use a Microsoft Entra Workload ID

A workload identity is an identity used by an application running on a pod that can authenticate itself against other Azure services that support it, such as Storage or SQL. It integrates with the capabilities native to Kubernetes to federate with external identity providers. In this security model, the AKS cluster acts as token issuer, Microsoft Entra ID uses OpenID Connect to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. Your workload can exchange a service account token projected to its volume for a Microsoft Entra token using the Azure Identity client library using the [Azure SDK](https://azure.microsoft.com/downloads/) or the [Microsoft Authentication Library](/en-us/azure/active-directory/develop/msal-overview) (MSAL).

For more information about workload identities, see [Configure an AKS cluster to use Microsoft Entra Workload ID with your applications](workload-identity-overview)

#### Use Azure Key Vault with Secrets Store CSI Driver

Using the [Microsoft Entra Workload ID](workload-identity-overview) enables authentication against supporting Azure services. For your own services or applications without managed identities for Azure resources, you can still authenticate using credentials or keys. A digital vault can be used to store these secret contents.

When applications need a credential, they communicate with the digital vault, retrieve the latest secret contents, and then connect to the required service. Azure Key Vault can be this digital vault. The simplified workflow for retrieving a credential from Azure Key Vault using pod managed identities is shown in the following diagram:


With Key Vault, you store and regularly rotate secrets such as credentials, storage account keys, or certificates. You can integrate Azure Key Vault with an AKS cluster using the [Azure Key Vault provider for the Secrets Store CSI Driver](csi-secrets-store-driver). The Secrets Store CSI driver enables the AKS cluster to natively retrieve secret contents from Key Vault and securely provide them only to the requesting pod. Work with your cluster operator to deploy the Secrets Store CSI Driver onto AKS worker nodes. You can use a Microsoft Entra Workload ID to request access to Key Vault and retrieve the secret contents needed through the Secrets Store CSI Driver.

## Next steps

This article focused on how to secure your pods. To implement some of these areas, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption -->

# Enable KMS data encryption in Azure Kubernetes Service (AKS) clusters (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable Key Management Service (KMS) data encryption for Kubernetes secrets in Azure Kubernetes Service (AKS). KMS encryption encrypts Kubernetes secrets stored in etcd using Azure Key Vault keys.

AKS supports two key management options:

**Platform-managed keys (PMK)**: AKS automatically creates and manages the encryption keys. This option provides the simplest setup with automatic key rotation.**Customer-managed keys (CMK)**: You create and manage your own Azure Key Vault and encryption keys. This option provides full control over key lifecycle and meets compliance requirements that mandate customer-managed keys.

For more information about encryption concepts and key options, see [Data encryption at rest concepts for AKS](kms-data-encryption-concepts).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.73.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You need the
`aks-preview`

Azure CLI extension version*19.0.0b13*or later.- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
`kubectl`

CLI tool installed.

### Register the feature flag

To use KMS data encryption with platform-managed keys, register the `KMSPMKPreview`

feature flag in your subscription.

Register the feature flag using the

command.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name KMSPMKPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name KMSPMKPreview`

When the status shows

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Set up environment variables

Set up environment variables for your deployment. Replace the placeholder values with your own.

```
# Set environment variables
export SUBSCRIPTION_ID="<your-subscription-id>"
export RESOURCE_GROUP="<your-resource-group>"
export LOCATION="<your-location>"
export CLUSTER_NAME="<your-cluster-name>"
# Set subscription
az account set --subscription $SUBSCRIPTION_ID
# Create resource group if it doesn't exist
az group create --name $RESOURCE_GROUP --location $LOCATION
```


## Enable platform-managed key encryption

With platform-managed keys, AKS automatically creates and manages the Azure Key Vault and encryption keys. Key rotation is handled automatically by the platform.

### Create a new AKS cluster with platform-managed keys

Create a new AKS cluster with KMS encryption using platform-managed keys.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--generate-ssh-keys
```


### Enable platform-managed keys on an existing cluster

Enable KMS encryption with platform-managed keys on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Enable customer-managed key encryption with a private key vault

For enhanced security, you can use a private key vault that has public network access disabled. AKS accesses the private key vault through the [trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only). This section shows how to configure customer-managed keys with a private key vault.

### Create a key vault and key with trusted services access

Note

This section illustrates creating a key vault with public network access initially, then enabling the firewall with trusted services bypass. This approach is for illustrative purposes only. In production environments, you should create and manage your key vault as private from the start. For guidance on managing private key vaults, see [Azure Key Vault network security](/en-us/azure/key-vault/general/network-security).

Create a key vault with Azure RBAC enabled.

`export KEY_VAULT_NAME="<your-key-vault-name>" az keyvault create \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --enable-rbac-authorization true \ --public-network-access Enabled # Get the key vault resource ID export KEY_VAULT_RESOURCE_ID=$(az keyvault show --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --query id -o tsv)`

Assign yourself the Key Vault Crypto Officer role to create a key.

`az role assignment create \ --role "Key Vault Crypto Officer" \ --assignee-object-id $(az ad signed-in-user show --query id -o tsv) \ --assignee-principal-type "User" \ --scope $KEY_VAULT_RESOURCE_ID`

Create a key in the key vault.

`export KEY_NAME="<your-key-name>" az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT_NAME # Get the key ID (without version for automatic rotation) export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT_NAME --query 'key.kid' -o tsv) export KEY_ID_NO_VERSION=$(echo $KEY_ID | sed 's|/[^/]*$||')`

Enable the key vault firewall with trusted services bypass.

`az keyvault update \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --default-action Deny \ --bypass AzureServices`

The

`--default-action Deny`

parameter blocks public network access, and the`--bypass AzureServices`

parameter allows trusted Azure services (including AKS) to access the key vault.

### Create a user-assigned managed identity

Create a user-assigned managed identity for the cluster.

`export IDENTITY_NAME="<your-identity-name>" az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP # Get the identity details export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv)`

Assign the required roles to the managed identity.

`# Assign Key Vault Crypto User role for encrypt/decrypt operations az role assignment create \ --role "Key Vault Crypto User" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID # Assign Key Vault Contributor role for key management az role assignment create \ --role "Key Vault Contributor" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID`


### Create a new AKS cluster with customer-managed keys (private)

Create a new AKS cluster with KMS encryption using customer-managed keys with a private key vault.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Private \
--assign-identity $IDENTITY_RESOURCE_ID \
--generate-ssh-keys
```


### Enable customer-managed keys on an existing cluster (private)

Enable KMS encryption with customer-managed keys using a private key vault on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Private \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"azureKeyVaultKms": {
"enabled": true,
"keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>",
"keyVaultNetworkAccess": "Private",
"keyVaultResourceId": "<key-vault-resource-id>"
},
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Enable customer-managed key encryption with a public key vault

With customer-managed keys, you create and manage your own Azure Key Vault and encryption keys. This section shows how to configure customer-managed keys with a public key vault.

### Create a key vault and key

Create a key vault with Azure RBAC enabled.

`export KEY_VAULT_NAME="<your-key-vault-name>" az keyvault create \ --name $KEY_VAULT_NAME \ --resource-group $RESOURCE_GROUP \ --enable-rbac-authorization true \ --public-network-access Enabled # Get the key vault resource ID export KEY_VAULT_RESOURCE_ID=$(az keyvault show --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP --query id -o tsv)`

Assign yourself the Key Vault Crypto Officer role to create a key.

`az role assignment create \ --role "Key Vault Crypto Officer" \ --assignee-object-id $(az ad signed-in-user show --query id -o tsv) \ --assignee-principal-type "User" \ --scope $KEY_VAULT_RESOURCE_ID`

Create a key in the key vault.

`export KEY_NAME="<your-key-name>" az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT_NAME # Get the key ID (without version for automatic rotation) export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT_NAME --query 'key.kid' -o tsv) export KEY_ID_NO_VERSION=$(echo $KEY_ID | sed 's|/[^/]*$||')`


### Create a user-assigned managed identity

Create a user-assigned managed identity for the cluster.

`export IDENTITY_NAME="<your-identity-name>" az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP # Get the identity details export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv)`

Assign the required roles to the managed identity.

`# Assign Key Vault Crypto User role for encrypt/decrypt operations az role assignment create \ --role "Key Vault Crypto User" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID # Assign Key Vault Contributor role for key management az role assignment create \ --role "Key Vault Contributor" \ --assignee-object-id $IDENTITY_OBJECT_ID \ --assignee-principal-type "ServicePrincipal" \ --scope $KEY_VAULT_RESOURCE_ID`


### Create a new AKS cluster with customer-managed keys

Create a new AKS cluster with KMS encryption using customer-managed keys.

```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kubernetes-version 1.33.0 \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID \
--generate-ssh-keys
```


### Enable customer-managed keys on an existing cluster

Enable KMS encryption with customer-managed keys on an existing AKS cluster.

Note

The cluster must be running Kubernetes version 1.33 or later.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Verify KMS configuration

After enabling KMS encryption, verify the configuration.

```
az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query 'securityProfile'
```


The output includes the KMS configuration:

```
{
"azureKeyVaultKms": {
"enabled": true,
"keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>",
"keyVaultNetworkAccess": "Public",
"keyVaultResourceId": "<key-vault-resource-id>"
},
"kubernetesResourceObjectEncryptionProfile": {
"infrastructureEncryption": "Enabled"
}
}
```


## Migrate between key management options

You can migrate between platform-managed keys and customer-managed keys.

### Migrate from platform-managed keys to customer-managed keys

To migrate from platform-managed keys to customer-managed keys, first set up the key vault, key, and managed identity as described in the customer-managed keys section, then run the update command:

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--enable-azure-keyvault-kms \
--azure-keyvault-kms-key-id $KEY_ID_NO_VERSION \
--azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \
--azure-keyvault-kms-key-vault-network-access Public \
--assign-identity $IDENTITY_RESOURCE_ID
```


### Migrate from customer-managed keys to platform-managed keys

To migrate from customer-managed keys to platform-managed keys:

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--kms-infrastructure-encryption Enabled \
--disable-azure-keyvault-kms
```


## Key rotation

With KMS data encryption, key rotation is handled differently depending on your key management option:

**Platform-managed keys**: Key rotation is automatic. No action is required.**Customer-managed keys**: When you rotate the key version in Azure Key Vault, the KMS controller detects the rotation periodically (every 6 hours) and uses the new key version.

Note

Unlike the legacy KMS experience, with this new implementation you don't need to manually re-encrypt secrets after key rotation. The platform handles this automatically.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-app-cluster-reliability -->

# Deployment and cluster reliability best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides best practices for cluster reliability implemented both at a deployment and cluster level for your Azure Kubernetes Service (AKS) workloads. The article is intended for cluster operators and developers who are responsible for deploying and managing applications in AKS.

The best practices in this article are organized into the following categories:

## Deployment level best practices

The following deployment level best practices help ensure high availability and reliability for your AKS workloads. These best practices are local configurations that you can implement in the YAML files for your pods and deployments.

Note

Make sure you implement these best practices every time you deploy an update to your application. If not, you might experience issues with your application's availability and reliability, such as unintentional application downtime.

### Pod CPU and memory limits


Best practice guidanceSet pod CPU and memory limits for all pods to ensure that pods don't consume all resources on a node and to provide protection during service threats, such as DDoS attacks.


Pod CPU and memory limits define the maximum amount of CPU and memory a pod can use. When a pod exceeds its defined limits, it gets marked for removal. For more information, see [CPU resource units in Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-cpu) and [Memory resource units in Kubernetes](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#meaning-of-memory).

Setting CPU and memory limits helps you maintain node health and minimizes impact to other pods on the node. Avoid setting a pod limit higher than your nodes can support. Each AKS node reserves a set amount of CPU and memory for the core Kubernetes components. If you set a pod limit higher than the node can support, your application might try to consume too many resources and negatively impact other pods on the node. Cluster administrators need to set resource quotas on a namespace that requires setting resource requests and limits. For more information, see [Enforce resource quotas in AKS](operator-best-practices-scheduler#enforce-resource-quotas).

In the following example pod definition file, the `resources`

section sets the CPU and memory limits for the pod:

```
kind: Pod
apiVersion: v1
metadata:
name: mypod
spec:
containers:
- name: mypod
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
```


Tip

You can use the `kubectl describe node`

command to view the CPU and memory capacity of your nodes, as shown in the following example:

```
kubectl describe node <node-name>
# Example output
Capacity:
cpu: 8
ephemeral-storage: 129886128Ki
hugepages-1Gi: 0
hugepages-2Mi: 0
memory: 32863116Ki
pods: 110
Allocatable:
cpu: 7820m
ephemeral-storage: 119703055367
hugepages-1Gi: 0
hugepages-2Mi: 0
memory: 28362636Ki
pods: 110
```


For more information, see [Assign CPU Resources to Containers and Pods](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) and [Assign Memory Resources to Containers and Pods](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/).

### Vertical Pod Autoscaler (VPA)


Best practice guidanceUse Vertical Pod Autoscaler (VPA) to automatically adjust CPU and memory requests for your pods based on their actual usage.


While not directly implemented through the pod YAML, the Vertical Pod Autoscaler (VPA) helps optimize resource allocation by automatically adjusting the CPU and memory requests for your pods. This ensures that your applications have the resources they need to run efficiently without overprovisioning or underprovisioning.

VPA operates in three modes:

**Off**: Only provides recommendations without applying changes.**Auto**: Automatically updates pod resource requests during pod restarts.**Initial**: Sets resource requests only during pod creation.

The following example shows how to configure a VPA resource in Kubernetes:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: my-vpa
spec:
targetRef:
apiVersion: "apps/v1"
kind: Deployment
name: my-deployment
updatePolicy:
updateMode: "Auto" # Options: Off, Auto, Initial
```


For more information, see [Vertical Pod Autoscaler documentation](https://github.com/kubernetes/autoscaler/tree/master/vertical-pod-autoscaler).

### Pod Disruption Budgets (PDBs)


Best practice guidanceUse Pod Disruption Budgets (PDBs) to ensure that a minimum number of pods remain available during

voluntary disruptions, such as upgrade operations or accidental pod deletions.

[Pod Disruption Budgets (PDBs)](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/#pod-disruption-budgets) allow you to define how deployments or replica sets respond during voluntary disruptions, such as upgrade operations or accidental pod deletions. Using PDBs, you can define a minimum or maximum unavailable resource count. PDBs only affect the Eviction API for voluntary disruptions.

For example, let's say you need to perform a cluster upgrade and already have a PDB defined. Before performing the cluster upgrade, the Kubernetes scheduler ensures that the minimum number of pods defined in the PDB are available. If the upgrade would cause the number of available pods to fall below the minimum defined in the PDBs, the scheduler schedules extra pods on other nodes before allowing the upgrade to proceed. If you don't set a PDB, the scheduler doesn't have any constraints on the number of pods that can be unavailable during the upgrade, which can lead to a lack of resources and potential cluster outages.

In the following example PDB definition file, the `minAvailable`

field sets the minimum number of pods that must remain available during voluntary disruptions. The value can be an absolute number (for example, *3*) or a percentage of the desired number of pods (for example, *10%*).

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: mypdb
spec:
minAvailable: 3 # Minimum number of pods that must remain available during voluntary disruptions
selector:
matchLabels:
app: myapp
```


For more information, see [Plan for availability using PDBs](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets) and [Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

### Graceful termination for pods


Best practice guidanceUtilize

`PreStop`

hooks and configure an appropriate`terminationGracePeriodSeconds`

value to ensure pods are terminated gracefully.

Graceful termination ensures that pods are given enough time to clean up resources, complete ongoing tasks, or notify dependent services before being terminated. This is particularly important for stateful applications or services that require proper shutdown procedures.

#### Using `PreStop`

hooks

A `PreStop`

hook is called immediately before a container is terminated due to an API request or management event, such as preemption, resource contention, or a liveness/startup probe failure. The `PreStop`

hook allows you to define custom commands or scripts to execute before the container is stopped. For example, you can use it to flush logs, close database connections, or notify other services of the shutdown.

The following example pod definition file shows how to use a `PreStop`

hook to ensure graceful termination of a container:

```
apiVersion: v1
kind: Pod
metadata:
name: lifecycle-demo
spec:
containers:
- name: lifecycle-demo-container
image: nginx
lifecycle:
preStop:
exec:
command: ["/bin/sh", "-c", "nginx -s quit; while killall -0 nginx; do sleep 1; done"]
```


#### Configuring `terminationGracePeriodSeconds`


The `terminationGracePeriodSeconds`

field specifies the amount of time Kubernetes waits before forcefully terminating a pod. This period includes the time taken to execute the `PreStop`

hook. If the `PreStop`

hook doesn't complete within the grace period, the pod is forcefully terminated.

For example, the following pod definition sets a termination grace period of 30 seconds:

```
apiVersion: v1
kind: Pod
metadata:
name: example-pod
spec:
terminationGracePeriodSeconds: 30
containers:
- name: example-container
image: nginx
```


For more information, see [Container lifecycle hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/#container-hooks) and [Termination of Pods](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/#pod-termination).

### High availability during upgrades

#### Using `maxSurge`

for faster updates


Best practice guidanceConfigure the

`maxSurge`

field to allow additional pods to be created during rolling updates, enabling faster updates with minimal downtime.

The `maxSurge`

field specifies the maximum number of additional pods that can be created beyond the desired number of pods during a rolling update. This allows new pods to be created and become ready before old pods are terminated, ensuring faster updates and reducing the risk of downtime.

The following example deployment manifest demonstrates how to configure `maxSurge`

:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
strategy:
type: RollingUpdate
rollingUpdate:
maxSurge: 33% # Maximum number of additional pods created during the update
```


By setting `maxSurge`

to 3, this configuration ensures that up to three additional pods can be created during the rolling update, speeding up the deployment process while maintaining availability of your application.
For more information, see [Rolling Updates in Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment).

#### Using `maxUnavailable`

for controlled updates


Best practice guidanceConfigure the

`maxUnavailable`

field to limit the number of pods that can be unavailable during rolling updates, ensuring your application remains operational with minimal disruption.

The `maxUnavailable`

field is particularly useful for applications that require are compute intensive or have specific infrastructure needs. It specifies the maximum number of pods that can be unavailable at any given time during a rolling update. This ensures that a portion of your application remains functional while new pods are being deployed and old ones are terminated.

You can set `maxUnavailable`

as an absolute number (e.g., `1`

) or a percentage of the desired number of pods (e.g., `25%`

). For example, if your application has four replicas and you set `maxUnavailable`

to `1`

, Kubernetes ensures that at least three pods remain available during the update process.

The following example deployment manifest demonstrates how to configure `maxUnavailable`

:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 4
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
strategy:
type: RollingUpdate
rollingUpdate:
maxUnavailable: 1 # Maximum number of pods that can be unavailable during the update
```


In this example, setting `maxUnavailable`

to `1`

ensures that no more than one pod is unavailable at any given time during the rolling update. This configuration is ideal for applications which require specialized compute, where maintaining a minimum level of service availability is critical.

For more information, see [Rolling Updates in Kubernetes](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#rolling-update-deployment).

### Pod topology spread constraints


Best practice guidanceUse pod topology spread constraints to ensure that pods are spread across different nodes or zones to improve availability and reliability.


You can use pod topology spread constraints to control how pods are spread across your cluster based on the topology of the nodes and spread pods across different nodes or zones to improve availability and reliability.

The following example pod definition file shows how to use the `topologySpreadConstraints`

field to spread pods across different nodes:

```
apiVersion: v1
kind: Pod
metadata:
name: example-pod
spec:
# Configure a topology spread constraint
topologySpreadConstraints:
- maxSkew: <integer>
minDomains: <integer> # optional
topologyKey: <string>
whenUnsatisfiable: <string>
labelSelector: <object>
matchLabelKeys: <list> # optional
nodeAffinityPolicy: [Honor|Ignore] # optional
nodeTaintsPolicy: [Honor|Ignore] # optional
```


For more information, see [Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/).

### Readiness, liveness, and startup probes


Best practice guidanceConfigure readiness, liveness, and startup probes when applicable to improve resiliency for high loads and lower container restarts.


#### Readiness probes

In Kubernetes, the kubelet uses readiness probes to know when a container is ready to start accepting traffic. A pod is considered *ready* when all of its containers are ready. When a pod is *not ready*, it's removed from service load balancers. For more information, see [Readiness Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-readiness-probes).

The following example pod definition file shows a readiness probe configuration:

```
readinessProbe:
exec:
command:
- cat
- /tmp/healthy
initialDelaySeconds: 5
periodSeconds: 5
```


For more information, see [Configure readiness probes](/en-us/azure/container-instances/container-instances-readiness-probe).

#### Liveness probes

In Kubernetes, the kubelet uses liveness probes to know when to restart a container. If a container fails its liveness probe, the container is restarted. For more information, see [Liveness Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/).

The following example pod definition file shows a liveness probe configuration:

```
livenessProbe:
exec:
command:
- cat
- /tmp/healthy
```


Another kind of liveness probe uses an HTTP GET request. The following example pod definition file shows an HTTP GET request liveness probe configuration:

```
apiVersion: v1
kind: Pod
metadata:
labels:
test: liveness
name: liveness-http
spec:
containers:
- name: liveness
image: registry.k8s.io/liveness
args:
- /server
livenessProbe:
httpGet:
path: /healthz
port: 8080
httpHeaders:
- name: Custom-Header
value: Awesome
initialDelaySeconds: 3
periodSeconds: 3
```


For more information, see [Configure liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) and [Define a liveness HTTP request](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-a-liveness-http-request).

#### Startup probes

In Kubernetes, the kubelet uses startup probes to know when a container application has started. When you configure a startup probe, readiness and liveness probes don't start until the startup probe succeeds, ensuring the readiness and liveness probes don't interfere with application startup. For more information, see [Startup Probes in Kubernetes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/#define-startup-probes).

The following example pod definition file shows a startup probe configuration:

```
startupProbe:
httpGet:
path: /healthz
port: 8080
failureThreshold: 30
periodSeconds: 10
```


### Multi-replica applications


Best practice guidanceDeploy at least two replicas of your application to ensure high availability and resiliency in node-down scenarios.


In Kubernetes, you can use the `replicas`

field in your deployment to specify the number of pods you want to run. Running multiple instances of your application helps ensure high availability and resiliency in node-down scenarios. If you have [availability zones](#availability-zones) enabled, you can use the `replicas`

field to specify the number of pods you want to run across multiple availability zones.

The following example pod definition file shows how to use the `replicas`

field to specify the number of pods you want to run:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-deployment
labels:
app: nginx
spec:
replicas: 3
selector:
matchLabels:
app: nginx
template:
metadata:
labels:
app: nginx
spec:
containers:
- name: nginx
image: nginx:1.14.2
ports:
- containerPort: 80
```


For more information, see [Recommended active-active high availability solution overview for AKS](active-active-solution) and [Replicas in Deployment Specs](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/#replicas).

## Cluster and node pool level best practices

The following cluster and node pool level best practices help ensure high availability and reliability for your AKS clusters. You can implement these best practices when creating or updating your AKS clusters.

### Availability zones


Best practice guidanceUse multiple availability zones when creating an AKS cluster to ensure high availability in zone-down scenarios. Keep in mind that you can't change the availability zone configuration after creating the cluster.


[Availability zones](/en-us/azure/reliability/availability-zones-overview) are separated groups of datacenters within a region. These zones are close enough to have low-latency connections to each other, but far enough apart to reduce the likelihood that more than one zone is affected by local outages or weather. Using availability zones helps your data stay synchronized and accessible in zone-down scenarios. For more information, see [Running in multiple zones](https://kubernetes.io/docs/setup/best-practices/multiple-zones/).

### Cluster autoscaling


Best practice guidanceUse cluster autoscaling to ensure that your cluster can handle increased load and to reduce costs during low load.


To keep up with application demands in AKS, you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects issues, it scales up the number of nodes in the node pool to meet the application demand. It also regularly checks nodes for a lack of running pods and scales down the number of nodes as needed. For more information, see [Cluster autoscaling in AKS](cluster-autoscaler-overview).

You can use the `--enable-cluster-autoscaler`

parameter when creating an AKS cluster to enable the cluster autoscaler, as shown in the following example:

```
az aks create \
--resource-group myResourceGroup \
--name myAKSCluster \
--node-count 2 \
--vm-set-type VirtualMachineScaleSets \
--load-balancer-sku standard \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--generate-ssh-keys
```


You can also enable the cluster autoscaler on an existing node pool and configure more granular details of the cluster autoscaler by changing the default values in the cluster-wide autoscaler profile.

For more information, see [Use the cluster autoscaler in AKS](cluster-autoscaler).

### Standard Load Balancer


Best practice guidanceUse the Standard Load Balancer to provide greater reliability and resources, support for multiple availability zones, HTTP probes, and functionality across multiple data centers.


In Azure, the [Standard Load Balancer](/en-us/azure/load-balancer/skus) SKU is designed to be equipped for load balancing network layer traffic when high performance and low latency are needed. The Standard Load Balancer routes traffic within and across regions and to availability zones for high resiliency. The Standard SKU is the recommended and default SKU to use when creating an AKS cluster.

Important

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). We recommend that you use the Standard Load Balancer for new deployments and upgrade existing deployments to the Standard Load Balancer. For more information, see [Upgrading from Basic Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance).

The following example shows a `LoadBalancer`

service manifest that uses the Standard Load Balancer:

```
apiVersion: v1
kind: Service
metadata:
annotations:
service.beta.kubernetes.io/azure-load-balancer-ipv4 # Service annotation for an IPv4 address
name: azure-load-balancer
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-load-balancer
```


For more information, see [Use a standard load balancer in AKS](load-balancer-standard).

Tip

You can also use an [ingress controller](app-routing) or a [service mesh](istio-deploy-ingress) to manage network traffic, with each option providing different features and capabilities.

### System node pools

#### Use dedicated system node pools


Best practice guidanceUse system node pools to ensure no other user applications run on the same nodes, which can cause resource scarcity and impact system pods.


Use dedicated system node pools to ensure no other user application runs on the same nodes, which can cause scarcity of resources and potential cluster outages because of race conditions. To use a dedicated system node pool, you can use the `CriticalAddonsOnly`

taint on the system node pool. For more information, see [Use system node pools in AKS](use-system-pools#system-and-user-node-pools).

#### Autoscaling for system node pools


Best practice guidanceConfigure the autoscaler for system node pools to set minimum and maximum scale limits for the node pool.


Use the autoscaler on node pools to configure the minimum and maximum scale limits for the node pool. The system node pool should always be able to scale to meet the demands of system pods. If the system node pool is unable to scale, the cluster runs out of resources to help manage scheduling, scaling, and load balancing, which can lead to an unresponsive cluster.

For more information, see [Use the cluster autoscaler on node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

#### At least two nodes per system node pool


Best practice guidanceEnsure that system node pools have at least two nodes to ensure resiliency against freeze/upgrade scenarios, which can lead to nodes being restarted or shut down.


System node pools are used to run system pods, such as the kube-proxy, coredns, and the Azure CNI plugin. We recommend that you * ensure that system node pools have at least two nodes* to ensure resiliency against freeze/upgrade scenarios, which can lead to nodes being restarted or shut down. For more information, see

[Manage system node pools in AKS](use-system-pools).

### Upgrade configurations for node pools

#### Using `maxSurge`

for node pool upgrades


Best practice guidanceConfigure the

`maxSurge`

setting for node pool upgrades to improve reliability and minimize downtime during upgrade operations.

The `maxSurge`

setting specifies the maximum number of additional nodes that can be created during an upgrade. This ensures that new nodes are provisioned and ready before old nodes are drained and removed, reducing the risk of application downtime.

For example, the following Azure CLI command sets `maxSurge`

to 1 for a node pool:

```
az aks nodepool update \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name myNodePool \
--max-surge 1
```


By configuring `maxSurge`

, you can ensure that upgrades are performed faster while maintaining application availability.

For more information, see [Upgrade node pools in AKS](upgrade-cluster).

#### Using `maxUnavailable`

for node pool upgrades


Best practice guidanceConfigure the

`maxUnavailable`

setting for node pool upgrades to ensure application availability during upgrade operations.

The `maxUnavailable`

setting specifies the maximum number of nodes that can be unavailable during an upgrade. This ensures that a portion of your node pool remains operational while nodes are being upgraded.

For example, the following Azure CLI command sets `maxUnavailable`

to 1 for a node pool:

```
az aks nodepool update \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name myNodePool \
--max-unavailable 1
```


By configuring `maxUnavailable`

, you can control the impact of upgrades on your workloads, ensuring that sufficient resources remain available during the process.

For more information, see [Upgrade node pools in AKS](upgrade-cluster).


Best practice guidanceUse Accelerated Networking to provide lower latency, reduced jitter, and decreased CPU utilization on your VMs.


Accelerated Networking enables [single root I/O virtualization (SR-IOV)](/en-us/windows-hardware/drivers/network/overview-of-single-root-i-o-virtualization--sr-iov-) on [supported VM types](/en-us/azure/virtual-network/accelerated-networking-overview#supported-vm-instances), greatly improving networking performance.

The following diagram illustrates how two VMs communicate with and without Accelerated Networking:


For more information, see [Accelerated Networking overview](/en-us/azure/virtual-network/accelerated-networking-overview).

### Image versions


Best practice guidanceImages shouldn't use the

`latest`

tag.

#### Container image tags

Using the `latest`

tag for [container images](https://kubernetes.io/docs/concepts/containers/images/) can lead to unpredictable behavior and makes it difficult to track which version of the image is running in your cluster. You can minimize these risks by integrating and running scan and remediation tools in your containers at build and runtime. For more information, see [Best practices for container image management in AKS](operator-best-practices-container-image-management).

#### Node image upgrades

AKS provides multiple auto-upgrade channels for node OS image upgrades. You can use these channels to control the timing of upgrades. We recommend joining these auto-upgrade channels to ensure that your nodes are running the latest security patches and updates. For more information, see [Auto-upgrade node OS images in AKS](auto-upgrade-node-os-image).

### Standard tier for production workloads


Best practice guidanceUse the Standard tier for product workloads for greater cluster reliability and resources, support for up to 5,000 nodes in a cluster, and Uptime SLA enabled by default. If you need LTS, consider using the Premium tier.


The Standard tier for Azure Kubernetes Service (AKS) provides a financially backed 99.9% uptime [service-level agreement (SLA)](https://www.azure.cn/en-us/support/sla/kubernetes-service/) for your production workloads. The standard tier also provides greater cluster reliability and resources, support for up to 5,000 nodes in a cluster, and Uptime SLA enabled by default. For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

### Azure CNI for dynamic IP allocation


Best practice guidanceConfigure Azure CNI for dynamic IP allocation for better IP utilization and to prevent IP exhaustion for AKS clusters.


The dynamic IP allocation capability in Azure CNI allocates pod IPs from a subnet separate from the subnet hosting the AKS cluster and offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pod are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this solution.

For more information, see [Configure Azure CNI networking for dynamic allocation of IPs and enhanced subnet support](configure-azure-cni-dynamic-ip-allocation).

### v5 SKU VMs


Best practice guidanceUse v5 VM SKUs for improved performance during and after updates, less overall impact, and a more reliable connection for your applications.


For node pools in AKS, use v5 SKU VMs with ephemeral OS disks to provide sufficient compute resources for kube-system pods. For more information, see [Best practices for performance and scaling large workloads in AKS](best-practices-performance-scale-large).

### Do *not* use B series VMs


Best practice guidanceDon't use B series VMs for AKS clusters because they're low performance and don't work well with AKS.


B series VMs are low performance and don't work well with AKS. Instead, we recommend using [v5 SKU VMs](#v5-sku-vms).

### Premium Disks


Best practice guidanceUse Premium Disks to achieve 99.9% availability in one virtual machine (VM).


[Azure Premium Disks](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) offer a consistent submillisecond disk latency and high IOPS and throughout. Premium Disks are designed to provide low-latency, high-performance, and consistent disk performance for VMs.

The following example YAML manifest shows a [storage class definition](https://kubernetes.io/docs/concepts/storage/storage-classes/) for a premium disk:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: premium2-disk-sc
parameters:
cachingMode: None
skuName: PremiumV2_LRS
DiskIOPSReadWrite: "4000"
DiskMBpsReadWrite: "1000"
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
volumeBindingMode: Immediate
allowVolumeExpansion: true
```


For more information, see [Use Azure Premium SSD v2 disks on AKS](use-premium-v2-disks).

### Container Insights


Best practice guidanceEnable Container Insights to monitor and diagnose the performance of your containerized applications.


[Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview) is a feature of Azure Monitor that collects and analyzes container logs from AKS. You can analyze the collected data with a collection of [views](/en-us/azure/azure-monitor/containers/container-insights-analyze) and prebuilt [workbooks](/en-us/azure/azure-monitor/containers/container-insights-reports).

You can enable Container Insights monitoring on your AKS cluster using various methods. The following example shows how to enable Container Insights monitoring on an existing cluster using the Azure CLI:

```
az aks enable-addons -a monitoring --name myAKSCluster --resource-group myResourceGroup
```


For more information, see [Enable monitoring for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable).

### Azure Policy


Best practice guidanceApply and enforce security and compliance requirements for your AKS clusters using Azure Policy.


You can apply and enforce built-in security policies on your AKS clusters using [Azure Policy](/en-us/azure/governance/policy/overview). Azure Policy helps enforce organizational standards and assess compliance at-scale. After you install the [Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes), you can apply individual policy definitions or groups of policy definitions called initiatives to your clusters.

For more information, see [Secure your AKS clusters with Azure Policy](use-azure-policy).

## Next steps

This article focused on best practices for deployment and cluster reliability for Azure Kubernetes Service (AKS) clusters. For more best practices, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overview -->

# Azure Kubernetes Service (AKS) CNI networking overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes uses Container Networking Interface (CNI) plugins to manage networking in Kubernetes clusters. CNI plug-ins are responsible for assigning IP addresses to pods, network routing between pods, Kubernetes service routing, and more.

Azure Kubernetes Service (AKS) provides multiple CNI plugins that you can use in your clusters, depending on your networking requirements.

## Networking models in AKS

Choosing a CNI plugin for your AKS cluster largely depends on which networking model fits your needs best. Each model has its own advantages and disadvantages that you should consider when planning your AKS cluster.

AKS uses two main networking models:

**Overlay network**:- Conserves IP address space for virtual networks by using logically separate Classless Inter-Domain Routing (CIDR) ranges for pods.
- Provides maximum cluster scale support.
- Provides simple management of IP addresses.

**Flat network**:- Provides full virtual network connectivity for pods. Pods can be directly reached via their private IP address from connected networks.
- Requires large, non-fragmented IP address space for virtual networks.


Both networking models have multiple supported options for CNI plugins. The main differences between the models are how pod IP addresses are assigned and how traffic leaves the cluster.

### Overlay networks

Overlay networking is the most common networking model used in Kubernetes. In overlay networks, pods receive an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This configuration allows for simpler and often better scalability than the flat network model.

In overlay networks, pods can communicate with each other directly. Traffic that leaves the cluster is Source Network Address Translated (SNAT'd) to the node's IP address. Inbound pod IP traffic is routed through a service, such as a load balancer. The pod IP address is then "hidden" behind the node's IP address. This approach reduces the number of IP addresses required for virtual networks in your clusters.


For overlay networking, AKS provides the [Azure CNI Overlay](concepts-network-azure-cni-overlay) plugin. We recommend this CNI plugin for most scenarios.

### Flat networks

Unlike an overlay network, a flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Traffic that leaves your clusters is not SNAT'd, and the pod IP address is directly exposed to the destination. This approach can be useful for some scenarios, such as when you need to expose pod IP addresses to external services.


AKS provides two CNI plugins for flat networking:

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), the recommended CNI plugin for flat networking scenarios.[Azure CNI Node Subnet](concepts-network-legacy-cni#azure-cni-node-subnet), a legacy CNI model for flat networks. In general, we recommend that you use it only if you*need*a managed virtual network for your cluster.

## Choosing a CNI plugin

When you're choosing a CNI plugin, there are several factors to consider. Each networking model has its own advantages and disadvantages. The best choice for your cluster depends on your specific requirements.

### Use case comparison

| CNI plugin | Networking model | Use case highlights |
|---|---|---|
| Azure CNI Overlay | Overlay | - Best for conserving IPs for virtual networks - Maximum node count supported by API server plus 250 pods per node - Simpler configuration - No direct external pod IP access |
| Azure CNI Pod Subnet | Flat | - Direct external pod access - Modes for efficient IP usage for virtual networks or large cluster scale support (preview) |
| Kubenet (legacy) | Overlay | - Prioritization of IP conservation - Limited scale - Manual route management |
| Azure CNI Node Subnet (legacy) | Flat | - Direct external pod access - Simpler configuration - Limited scale - Inefficient use of IPs for virtual networks |

### Feature comparison

| Feature | Azure CNI Overlay | Azure CNI Pod Subnet | Azure CNI Node Subnet (legacy) | Kubenet (legacy) |
|---|---|---|---|---|
| Deployment of a cluster in an existing or new virtual network | Supported | Supported | Supported | Supported with manual user-defined routes (UDRs) |
| Connectivity between pod and virtual machine (VM), with the VM in the same virtual network or a peered virtual network | Pod initiated | Both ways | Both ways | Pod initiated |
| On-premises access via virtual private network (VPN) and Azure ExpressRoute | Pod initiated | Both ways | Both ways | Pod initiated |
| Access to service endpoints | Supported | Supported | Supported | Supported |
| Exposure of services via load balancer | Supported | Supported | Supported | Supported |
| Exposure of services via Azure Application Gateway ingress controller | Supported | Supported | Supported | Supported |
| Exposure of services via Application Gateway for Containers | Supported | Supported | Supported | Not Supported |
| Windows node pools | Supported | Supported | Supported | Not supported |
| Default Azure DNS and private zones | Supported | Supported | Supported | Supported |
| Sharing of virtual network subnets across multiple clusters | Supported | Supported | Supported | Not supported |

### Support scope between network models

Depending on the CNI plugin that you use, you can deploy the virtual network resources for your cluster in one of the following ways:

- The Azure platform can automatically create and configure the virtual network resources when you create an AKS cluster, like in Azure CNI Overlay, Azure CNI Node Subnet, and Kubenet.
- You can manually create and configure the virtual network resources and attach to those resources when you create your AKS cluster.

Although capabilities like service endpoints or UDRs are supported, the [support policies for AKS](support-policies) define what changes you can make. For example:

- If you manually create the virtual network resources for an AKS cluster, you're supported when configuring your own UDRs or service endpoints.
- If the Azure platform automatically creates the virtual network resources for your AKS cluster, you can't manually change those AKS-managed resources to configure your own UDRs or service endpoints.

## Prerequisites

When you're planning your network configuration for AKS, keep these requirements and considerations in mind:

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for address ranges for the Kubernetes service, pods, or cluster virtual networks. - In scenarios where you bring your own virtual network, the cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Authorization/roleAssignments/write`

`Microsoft.Network/virtualNetworks/subnets/read`

(needed only if you're defining your own subnets and CIDRs)

- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Azure network security groups overview](/en-us/azure/virtual-network/network-security-groups-overview).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/api-server-service-tags -->

# Use service tags for API server authorized IP ranges in Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Service tags for API server authorized IP ranges is a preview feature that allows you to use service tags to specify authorized IP ranges for the API server in Azure Kubernetes Service (AKS). This feature simplifies the management of authorized IP ranges by allowing you to use predefined service tags instead of manually specifying individual IP addresses or CIDR ranges.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - The
installed.`aks-preview`

Azure CLI extension - The
registered in your Azure subscription.`EnableServiceTagAuthorizedIPPreview`

feature flag

## Limitations

- This feature isn't compatible with
[API Server VNet Integration](api-server-vnet-integration). - Only one service tag is allowed in the
`--api-server-authorized-ip-ranges`

parameter. You can't specify multiple service tags.

## Install the `aks-preview`

Azure CLI extension

Install the Azure CLI preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update the extension to make sure you have the latest version using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the service tag authorized IP feature flag

Register the

`EnableServiceTagAuthorizedIPPreview`

feature flag using thecommand. It takes a few minutes for the registration to complete.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "EnableServiceTagAuthorizedIPPreview"`

Example output:

`{ "id": "/subscriptions/<subscription-id>/providers/Microsoft.ContainerService/features/EnableServiceTagAuthorizedIPPreview", "name": "EnableServiceTagAuthorizedIPPreview", "properties": { "state": "Registering" }, "type": "Microsoft.ContainerService/features" }`

Once the feature flag state changes from

`Registering`

to`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`

Verify the registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableServiceTagAuthorizedIPPreview"`

Example output:

`{ "id": "/subscriptions/<subscription-id>/providers/Microsoft.ContainerService/features/EnableServiceTagAuthorizedIPPreview", "name": "EnableServiceTagAuthorizedIPPreview", "properties": { "state": "Registered" }, "type": "Microsoft.ContainerService/features" }`


## Create an AKS cluster with service tag authorized IP ranges

Create a cluster with service tag authorized IP ranges using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the*myResourceGroup*resource group and authorizes the`AzureCloud`

service tag to allow all Azure services to access the API server and specify an extra IP address:`az aks create --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges AzureCloud,20.20.20.20`

Note

You should be able to curl the API server from an Azure virtual machine (VM) or Azure service that's part of the

`AzureCloud`

service tag.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/egress-udr -->

# Customize cluster egress with a user-defined routing table in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize the egress for your Azure Kubernetes Service (AKS) clusters to fit specific scenarios. AKS provisions a `Standard`

SKU load balancer for egress by default. However, the default setup may not meet the requirements of all scenarios if public IPs are disallowed or the scenario requires extra hops for egress.

This article walks through how to customize a cluster's egress route to support custom network scenarios. These scenarios include ones which disallow public IPs and require the cluster to sit behind a network virtual appliance (NVA).

## Prerequisites

- Azure CLI version 2.0.81 or greater. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - API version
`2020-01-01`

or greater.

## Requirements and limitations

Using outbound type is an advanced networking scenario and requires proper network configuration. The following requirements and limitations apply to using outbound type:

- Setting
`outboundType`

requires AKS clusters with a`vm-set-type`

of`VirtualMachineScaleSets`

and a`load-balancer-sku`

of`Standard`

. - Setting
`outboundType`

to a value of`UDR`

requires a user-defined route with valid outbound connectivity for the cluster. - Setting
`outboundType`

to a value of`UDR`

implies the ingress source IP routed to the load-balancer may**not match**the cluster's outgoing egress destination address.

## Overview of customizing egress with a user-defined routing table

AKS doesn't automatically configure egress paths if `userDefinedRouting`

is set, which means you must configure the egress.

When you don't use standard load balancer (SLB) architecture, you must establish explicit egress. You must deploy your AKS cluster into an existing virtual network with a subnet that has been previously configured. This architecture requires explicitly sending egress traffic to an appliance like a firewall, gateway, or proxy, so a public IP assigned to the standard load balancer or appliance can handle the Network Address Translation (NAT).

### Load balancer creation with `userDefinedRouting`


AKS clusters with an outbound type of UDR get a standard load balancer only when the first Kubernetes service of type `loadBalancer`

is deployed. The load balancer is configured with a public IP address for *inbound* requests and a backend pool for *inbound* requests. The Azure cloud provider configures inbound rules, but it **doesn't configure outbound public IP address or outbound rules**. Your UDR is the only source for egress traffic.

Note

Azure load balancers [don't incur a charge until a rule is placed](https://azure.microsoft.com/pricing/details/load-balancer/).

## Deploy a cluster with outbound type of UDR and Azure Firewall

To see an application of a cluster with outbound type using a user-defined route, see this [restrict egress traffic with Azure firewall example](limit-egress-traffic).

Important

Outbound type of UDR requires a route for 0.0.0.0/0 and a next hop destination of NVA in the route table.
The route table already has a default 0.0.0.0/0 to the Internet. Without a public IP address for Azure to use for Source Network Address Translation (SNAT), simply adding this route won't provide you outbound Internet connectivity. AKS validates that you don't create a 0.0.0.0/0 route pointing to the Internet but instead to a gateway, NVA, etc.
When using an outbound type of UDR, a load balancer public IP address for **inbound requests** isn't created unless you configure a service of type *loadbalancer*. AKS never creates a public IP address for **outbound requests** if you set an outbound type of UDR.

## Next steps

For more information on user-defined routes and Azure networking, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files -->

# Configure Azure NetApp Files for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods. A persistent volume can be used by one or many pods, and it can be statically or dynamically provisioned. This article shows you how to configure [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) to be used by pods on an Azure Kubernetes Service (AKS) cluster.

[Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) is an enterprise-class, high-performance, metered file storage service running on Azure and supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB). Kubernetes users have two options for using Azure NetApp Files volumes for Kubernetes workloads:

- Create Azure NetApp Files volumes
**statically**. In this scenario, the creation of volumes is external to AKS. Volumes are created using the Azure CLI or from the Azure portal, and are then exposed to Kubernetes by the creation of a`PersistentVolume`

. Statically created Azure NetApp Files volumes have many limitations (for example, inability to be expanded, needing to be over-provisioned, and so on). Statically created volumes aren't recommended for most use cases. - Create Azure NetApp Files volumes
**dynamically**, orchestrating through Kubernetes. This method is the**preferred**way to create multiple volumes directly through Kubernetes, and is achieved using[Trident](https://docs.netapp.com/us-en/trident/index.html). Trident is a CSI-compliant dynamic storage orchestrator that helps provision volumes natively through Kubernetes.

Note

Dual-protocol volumes can only be created **statically**. For more information on using dual-protocol volumes with Azure Kubernetes Service, see [Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol).

Using a CSI driver to directly consume Azure NetApp Files volumes from AKS workloads is the recommended configuration for most use cases. This requirement is accomplished using Trident, an open-source dynamic storage orchestrator for Kubernetes. Trident is an enterprise-grade storage orchestrator purpose-built for Kubernetes, and fully supported by NetApp. It simplifies access to storage from Kubernetes clusters by automating storage provisioning.

You can take advantage of Trident's Container Storage Interface (CSI) driver for Azure NetApp Files to abstract underlying details and create, expand, and snapshot volumes on-demand.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

The following considerations apply when you use Azure NetApp Files:

- Your AKS cluster must be
[in a region that supports Azure NetApp Files](https://azure.microsoft.com/global-infrastructure/services/?products=netapp®ions=all). - The Azure CLI version 2.0.59 or higher installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - After the initial deployment of an AKS cluster, you can choose to provision Azure NetApp Files volumes statically or dynamically.
- To use dynamic provisioning with Azure NetApp Files with Network File System (NFS), install and configure
[Trident](https://docs.netapp.com/us-en/trident/index.html)version 19.07 or higher. To use dynamic provisioning with Azure NetApp Files with Secure Message Block (SMB), install and configure Trident version 22.10 or higher. Dynamic provisioning for SMB shares is only supported on windows worker nodes. - Before you deploy Azure NetApp Files SMB volumes, you must identify the AD DS integration requirements for Azure NetApp Files to ensure that Azure NetApp Files is well connected to AD DS. For more information, see
[Understand guidelines for Active Directory Domain Services site design and planning](/en-us/azure/azure-netapp-files/understand-guidelines-active-directory-domain-service-site). Both the AKS cluster and Azure NetApp Files must have connectivity to the same AD.

## Configure Azure NetApp Files for AKS workloads

This section describes how to set up Azure NetApp Files for AKS workloads. It's applicable for all scenarios within this article.

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*poolsize*,*premium*,*myvnet*,*myANFSubnet*, and*myprefix*with appropriate values for your environment.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SIZE="poolsize" # size in TiB SERVICE_LEVEL="Premium" # valid values are Standard, Premium and Ultra VNET_NAME="myvnet" SUBNET_NAME="myANFSubnet" ADDRESS_PREFIX="myprefix"`

Register the

*Microsoft.NetApp*resource provider by running the following command:`az provider register --namespace Microsoft.NetApp --wait`

Note

This operation can take several minutes to complete.

Create a new account by using the command

. When you create an Azure NetApp account for use with AKS, you can create the account in an existing resource group or create a new one in the same region as the AKS cluster.`az netappfiles account create`

`az netappfiles account create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME`

Create a new capacity pool by using the command

. Replace the variables shown in the command with your Azure NetApp Files information. The`az netappfiles pool create`

`account_name`

should be the same as created in Step 3.`az netappfiles pool create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --size $SIZE \ --service-level $SERVICE_LEVEL`

Create a subnet to

[delegate to Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-delegate-subnet)using the command. Specify the resource group hosting the existing virtual network for your AKS cluster. Replace the variables shown in the command with your Azure NetApp Files information.`az network vnet subnet create`

Note

This subnet must be in the same virtual network as your AKS cluster.

`az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --delegations "Microsoft.Netapp/volumes" \ --address-prefixes $ADDRESS_PREFIX`


## Statically or dynamically provision Azure NetApp Files volumes for NFS or SMB

After you [configure Azure NetApp Files for AKS workloads](#configure-azure-netapp-files-for-aks-workloads), you can statically or dynamically provision Azure NetApp Files using NFS, SMB, or dual-protocol volumes within the capacity pool. Follow instructions in:

[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs)[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb)[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-cni-overview -->

# Azure Kubernetes Service (AKS) CNI networking overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes uses Container Networking Interface (CNI) plugins to manage networking in Kubernetes clusters. CNI plug-ins are responsible for assigning IP addresses to pods, network routing between pods, Kubernetes service routing, and more.

Azure Kubernetes Service (AKS) provides multiple CNI plugins that you can use in your clusters, depending on your networking requirements.

## Networking models in AKS

Choosing a CNI plugin for your AKS cluster largely depends on which networking model fits your needs best. Each model has its own advantages and disadvantages that you should consider when planning your AKS cluster.

AKS uses two main networking models:

**Overlay network**:- Conserves IP address space for virtual networks by using logically separate Classless Inter-Domain Routing (CIDR) ranges for pods.
- Provides maximum cluster scale support.
- Provides simple management of IP addresses.

**Flat network**:- Provides full virtual network connectivity for pods. Pods can be directly reached via their private IP address from connected networks.
- Requires large, non-fragmented IP address space for virtual networks.


Both networking models have multiple supported options for CNI plugins. The main differences between the models are how pod IP addresses are assigned and how traffic leaves the cluster.

### Overlay networks

Overlay networking is the most common networking model used in Kubernetes. In overlay networks, pods receive an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This configuration allows for simpler and often better scalability than the flat network model.

In overlay networks, pods can communicate with each other directly. Traffic that leaves the cluster is Source Network Address Translated (SNAT'd) to the node's IP address. Inbound pod IP traffic is routed through a service, such as a load balancer. The pod IP address is then "hidden" behind the node's IP address. This approach reduces the number of IP addresses required for virtual networks in your clusters.


For overlay networking, AKS provides the [Azure CNI Overlay](concepts-network-azure-cni-overlay) plugin. We recommend this CNI plugin for most scenarios.

### Flat networks

Unlike an overlay network, a flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Traffic that leaves your clusters is not SNAT'd, and the pod IP address is directly exposed to the destination. This approach can be useful for some scenarios, such as when you need to expose pod IP addresses to external services.


AKS provides two CNI plugins for flat networking:

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), the recommended CNI plugin for flat networking scenarios.[Azure CNI Node Subnet](concepts-network-legacy-cni#azure-cni-node-subnet), a legacy CNI model for flat networks. In general, we recommend that you use it only if you*need*a managed virtual network for your cluster.

## Choosing a CNI plugin

When you're choosing a CNI plugin, there are several factors to consider. Each networking model has its own advantages and disadvantages. The best choice for your cluster depends on your specific requirements.

### Use case comparison

| CNI plugin | Networking model | Use case highlights |
|---|---|---|
| Azure CNI Overlay | Overlay | - Best for conserving IPs for virtual networks - Maximum node count supported by API server plus 250 pods per node - Simpler configuration - No direct external pod IP access |
| Azure CNI Pod Subnet | Flat | - Direct external pod access - Modes for efficient IP usage for virtual networks or large cluster scale support (preview) |
| Kubenet (legacy) | Overlay | - Prioritization of IP conservation - Limited scale - Manual route management |
| Azure CNI Node Subnet (legacy) | Flat | - Direct external pod access - Simpler configuration - Limited scale - Inefficient use of IPs for virtual networks |

### Feature comparison

| Feature | Azure CNI Overlay | Azure CNI Pod Subnet | Azure CNI Node Subnet (legacy) | Kubenet (legacy) |
|---|---|---|---|---|
| Deployment of a cluster in an existing or new virtual network | Supported | Supported | Supported | Supported with manual user-defined routes (UDRs) |
| Connectivity between pod and virtual machine (VM), with the VM in the same virtual network or a peered virtual network | Pod initiated | Both ways | Both ways | Pod initiated |
| On-premises access via virtual private network (VPN) and Azure ExpressRoute | Pod initiated | Both ways | Both ways | Pod initiated |
| Access to service endpoints | Supported | Supported | Supported | Supported |
| Exposure of services via load balancer | Supported | Supported | Supported | Supported |
| Exposure of services via Azure Application Gateway ingress controller | Supported | Supported | Supported | Supported |
| Exposure of services via Application Gateway for Containers | Supported | Supported | Supported | Not Supported |
| Windows node pools | Supported | Supported | Supported | Not supported |
| Default Azure DNS and private zones | Supported | Supported | Supported | Supported |
| Sharing of virtual network subnets across multiple clusters | Supported | Supported | Supported | Not supported |

### Support scope between network models

Depending on the CNI plugin that you use, you can deploy the virtual network resources for your cluster in one of the following ways:

- The Azure platform can automatically create and configure the virtual network resources when you create an AKS cluster, like in Azure CNI Overlay, Azure CNI Node Subnet, and Kubenet.
- You can manually create and configure the virtual network resources and attach to those resources when you create your AKS cluster.

Although capabilities like service endpoints or UDRs are supported, the [support policies for AKS](support-policies) define what changes you can make. For example:

- If you manually create the virtual network resources for an AKS cluster, you're supported when configuring your own UDRs or service endpoints.
- If the Azure platform automatically creates the virtual network resources for your AKS cluster, you can't manually change those AKS-managed resources to configure your own UDRs or service endpoints.

## Prerequisites

When you're planning your network configuration for AKS, keep these requirements and considerations in mind:

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for address ranges for the Kubernetes service, pods, or cluster virtual networks. - In scenarios where you bring your own virtual network, the cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Authorization/roleAssignments/write`

`Microsoft.Network/virtualNetworks/subnets/read`

(needed only if you're defining your own subnets and CIDRs)

- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Azure network security groups overview](/en-us/azure/virtual-network/network-security-groups-overview).
