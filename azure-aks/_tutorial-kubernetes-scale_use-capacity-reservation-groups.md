---
merged_at: 2026-01-25T12:06:27.732187
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-scale -->

# Tutorial - Scale applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you followed the previous tutorials, you have a working Kubernetes cluster and Azure Store Front app.

In this tutorial, you scale out the pods in the app, try pod autoscaling, and scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads. You learn how to:

- Scale the Kubernetes nodes.
- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created an AKS cluster, deployed an application, and used Azure Service Bus to redeploy an updated application. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Manually scale pods

View the pods in your cluster using the

command.`kubectl get`

`kubectl get pods`

The following example output shows the pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE order-service-848767080-tf34m 1/1 Running 0 31m product-service-4019737227-2q2qz 1/1 Running 0 31m store-front-2606967446-2q2qz 1/1 Running 0 31m`

Manually change the number of pods in the

*store-front*deployment using thecommand.`kubectl scale`

`kubectl scale --replicas=5 deployment.apps/store-front`

Verify the additional pods were created using the

command.`kubectl get pods`

`kubectl get pods --selector app=store-front`

The following example output shows the additional pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE store-front-3309479140-2hfh0 1/1 Running 0 3m store-front-3309479140-bzt05 1/1 Running 0 3m store-front-3309479140-fvcvm 1/1 Running 0 3m store-front-3309479140-hrbf2 1/1 Running 0 15m store-front-3309479140-qphz8 1/1 Running 0 3m`


## Autoscale pods

To use the horizontal pod autoscaler, all containers must have defined CPU requests and limits, and pods must have specified requests. In the `aks-store-quickstart`

deployment, the *front-end* container requests 1m CPU with a limit of 1000m CPU.

These resource requests and limits are defined for each container, as shown in the following condensed example YAML:

```
...
containers:
- name: store-front
image: ghcr.io/azure-samples/aks-store-demo/store-front:latest
ports:
- containerPort: 8080
name: store-front
...
resources:
requests:
cpu: 1m
...
limits:
cpu: 1000m
...
```


### Autoscale pods using a manifest file

Create a manifest file to define the autoscaler behavior and resource limits, as shown in the following condensed example manifest file

`aks-store-quickstart-hpa.yaml`

:`apiVersion: autoscaling/v2 kind: HorizontalPodAutoscaler metadata: name: store-front-hpa spec: maxReplicas: 10 # define max replica count minReplicas: 3 # define min replica count scaleTargetRef: apiVersion: apps/v1 kind: Deployment name: store-front metrics: - type: Resource resource: name: cpu target: type: Utilization averageUtilization: 50`

Apply the autoscaler manifest file using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart-hpa.yaml`

Check the status of the autoscaler using the

`kubectl get hpa`

command.`kubectl get hpa`

After a few minutes, with minimal load on the Azure Store Front app, the number of pod replicas decreases to three. You can use

`kubectl get pods`

command again to see the unneeded pods being removed.

Note

You can enable the Kubernetes-based Event-Driven Autoscaler (KEDA) AKS add-on to your cluster to drive scaling based on the number of events needing to be processed. For more information, see [Enable simplified application autoscaling with the Kubernetes Event-Driven Autoscaling (KEDA) add-on (Preview)](keda-about).

## Manually scale AKS nodes

If you created your Kubernetes cluster using the commands in the previous tutorials, your cluster has two nodes. If you want to increase or decrease this amount, you can manually adjust the number of nodes.

The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*. The command takes a couple of minutes to complete.

Scale your cluster nodes using the

command.`az aks scale`

`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3`

Once the cluster successfully scales, your output will be similar to following example output:

`"aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { ... "count": 3, "mode": "System", "name": "nodepool1", "osDiskSizeGb": 128, "osDiskType": "Managed", "osType": "Linux", "ports": null, "vmSize": "Standard_DS2_v2", "vnetSubnetId": null ... } ... ]`


You can also autoscale the nodes in your cluster. For more information, see [Use the cluster autoscaler with node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

## Next steps

In this tutorial, you used different scaling features in your Kubernetes cluster. You learned how to:

- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.
- Manually scale the Kubernetes nodes.

In the next tutorial, you learn how to upgrade Kubernetes in your AKS cluster.


---

<!-- DOCUMENTO FUSIONADO: use-capacity-reservation-groups.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-capacity-reservation-groups -->

# Assign capacity reservation groups to Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your workload demands change, you can associate existing [capacity reservation groups (CRGs)](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set) to your Azure Kubernetes Service (AKS) node pools to guarantee allocated capacity for them. Capacity reservation groups allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. This feature is useful for workloads that require guaranteed capacity, such as those with predictable traffic patterns or those that need to meet specific performance requirements.

In this article, you learn how to use capacity reservation groups with node pools in AKS.

Note

Deleting a node pool implicitly dissociates that node pool from any associated capacity reservation group before the node pool is deleted. Deleting a cluster implicitly dissociates all node pools in that cluster from their associated capacity reservation groups.

## Prerequisites for using capacity reservation groups with AKS node pools

- You need the Azure CLI version 2.56 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need an existing
[capacity reservation group](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set)with at least one capacity reservation. If not, the node pool is added to the cluster with a warning and no capacity reservation group gets associated. - You need to
[create a user-assigned managed identity with the](#create-a-user-assigned-managed-identity-and-assign-it-to-an-aks-cluster)for the resource group that contains the capacity reservation group and assign the identity to your AKS cluster. System-assigned managed identities don't work for this feature.`Contributor`

role

### Create a user-assigned managed identity and assign it to an AKS cluster

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name <identity-name> --resource-group <resource-group-name> --location <location>`

Get the ID of the user-assigned managed identity using the

command and set it to an environment variable.`az identity show`

`IDENTITY_ID=$(az identity show --name <identity-name> --resource-group <resource-group-name> --query identity.id -o tsv)`

Assign the

`Contributor`

role to the user-assigned identity using thecommand.`az role assignment create`

`az role assignment create --assignee $IDENTITY_ID --role "Contributor" --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>`

It can take up to

*60 minutes*for the role assignment to propagate.Assign the user-assigned managed identity to a new or existing AKS cluster using the

`--assign-identity`

flag with theor`az aks create`

command.`az aks update`

`# Create a new AKS cluster with the user-assigned managed identity az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys # Update an existing AKS cluster to use the user-assigned managed identity az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> \ --node-count <node-count> \ --enable-managed-identity \ --assign-identity $IDENTITY_ID`


## Limitations for using capacity reservation groups with AKS node pools

You can't update an existing node pool with a capacity reservation group. Instead, you need to create a new node pool with the `--crg-id`

flag to associate it with the capacity reservation group. You can also associate an existing capacity reservation group with a system node pool during cluster creation.

## Get the ID of an existing capacity reservation group

Get the ID of an existing capacity reservation group using the

command and set it to an environment variable.`az capacity reservation group show`

`CRG_ID=$(az capacity reservation group show --capacity-reservation-group <crg-name> --resource-group <resource-group-name> --query id -o tsv)`


## Associate an existing capacity reservation group with a node pool

Associate an existing capacity reservation group with a node pool using the

command with the`az aks nodepool add`

`--crg-id`

flag. The following example assumes you have a CRG named "myCRG".`az aks nodepool add --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --crg-id $CRG_ID`


## Associate an existing capacity reservation group with a system node pool

To associate an existing capacity reservation group with a system node pool, you need to assign the user-assigned managed identity with the `Contributor`

role to the cluster during cluster creation. You can then use the `--crg-id`

flag to associate the capacity reservation group with the system node pool.

Create a new AKS cluster with the user-assigned managed identity and associate it with the capacity reservation group using the

`--assign-identity`

and`--crg-id`

flags with thecommand.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --crg-id $CRG_ID \ --generate-ssh-keys`


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).
