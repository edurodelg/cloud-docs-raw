---
merged_at: 2026-01-25T12:25:33.917591
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: coredns-troubleshoot.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/coredns-troubleshoot -->

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

<!-- DOCUMENTO FUSIONADO: use-azure-policy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-azure-policy -->

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
