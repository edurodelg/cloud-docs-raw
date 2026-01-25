---
merged_at: 2026-01-25T12:25:33.896978
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: customize-resource-configuration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).


---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-deploy-application.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application -->

# Tutorial - Deploy an application to Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. You build and deploy your own applications and services into a Kubernetes cluster and let the cluster manage the availability and connectivity.

In this tutorial, you deploy a sample application into a Kubernetes cluster. You learn how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

Tip

With AKS, you can use the following approaches for configuration management:

**GitOps**: Enables declarations of your cluster's state to automatically apply to the cluster. To learn how to use GitOps to deploy an application with an AKS cluster, see the[prerequisites for Azure Kubernetes Service clusters](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json#for-azure-kubernetes-service-clusters)in the[GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json)tutorial.**DevOps**: Enables you to build, test, and deploy with continuous integration (CI) and continuous delivery (CD). To see examples of how to use DevOps to deploy an application with an AKS cluster, see[Build and deploy to AKS with Azure Pipelines](devops-pipeline)or[GitHub Actions for deploying to Kubernetes](kubernetes-action).

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, and created a Kubernetes cluster. To complete this tutorial, you need the precreated `aks-store-quickstart.yaml`

Kubernetes manifest file. This file was downloaded in the application source code from [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update the manifest file

In these tutorials, your Azure Container Registry (ACR) instance stores the container images for the sample application. To deploy the application, you must update the image names in the Kubernetes manifest file to include your ACR login server name.

Get your login server address using the

command and query for your login server.`az acr list`

`az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table`

Make sure you're in the cloned

*aks-store-demo*directory, and then open the`aks-store-quickstart.yaml`

manifest file with a text editor.Update the

`image`

property for the containers by replacing*ghcr.io/azure-samples*with your ACR login server name.`containers: ... - name: order-service image: <acrName>.azurecr.io/aks-store-demo/order-service:latest ... - name: product-service image: <acrName>.azurecr.io/aks-store-demo/product-service:latest ... - name: store-front image: <acrName>.azurecr.io/aks-store-demo/store-front:latest ...`

Save and close the file.


## Run the application

Deploy the application using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the resources successfully created in the AKS cluster:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`

Check the deployment is successful by viewing the pods with the

`kubectl get pods`

command.`kubectl get pods`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

### Command Line

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

Initially, the

`EXTERNAL-IP`

for the`store-front`

service shows as`<pending>`

:`store-front LoadBalancer 10.0.34.242 <pending> 80:30676/TCP 5s`

When the

`EXTERNAL-IP`

address changes from`<pending>`

to a public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`store-front LoadBalancer 10.0.34.242 52.179.23.131 80:30676/TCP 67s`

View the application in action by opening a web browser and navigating to the external IP address of your service:

`http://<external-ip>`

.

If the application doesn't load, it might be an authorization problem with your image registry. To view the status of your containers, use the `kubectl get pods`

command. If you can't pull the container images, see [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration).

### Azure portal

Navigate to the Azure portal to find your deployment information.

Navigate to your AKS cluster resource.

From the service menu, under

**Kubernetes Resources**, select**Services and ingresses**.Copy the External IP shown in the column for the

`store-front`

service.Paste the IP into your browser to visit your store page.


## Clean up resources

Since you validated the application's functionality, you can now remove the cluster from the application. We will deploy the application again in the next tutorial.

Stop and remove the container instances and resources using the

`kubectl delete`

command.`kubectl delete -f aks-store-quickstart.yaml`

Check that all the application pods have been removed using the

`kubectl get pods`

command.`kubectl get pods`


## Next steps

In this tutorial, you deployed a sample Azure application to a Kubernetes cluster in AKS. You learned how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

In the next tutorial, you learn how to use PaaS services for stateful workloads in Kubernetes.
