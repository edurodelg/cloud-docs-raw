---
merged_at: 2026-01-25T12:06:27.688002
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: delete-node-pool.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/delete-node-pool -->

# Delete an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines node pool deletion in Azure Kubernetes Service (AKS), including what happens when you delete a node pool and how to delete a node pool.

## What happens when you delete a node pool?

When you delete a node pool, the following resources are deleted:

- The virtual machine scale set (VMSS) and virtual machines (VMs) for each node in the node pool
- Any node instances in the node pool along with any pods running on those nodes

## Delete a node pool

Important

Keep the following information in mind when deleting a node pool:

**You can't recover a node pool after it's deleted**. You need to create a new node pool and redeploy your applications.

Delete a node pool using the [ az aks nodepool delete](/en-us/cli/azure/aks#az-aks-nodepool-delete) command.

```
az aks nodepool delete \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name>
```


To verify that the node pool was deleted successfully, use the `kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Ignore PodDisruptionBudgets (PDBs) when removing an existing node pool

If your cluster has PodDisruptionBudgets that are preventing the deletion of the node pool, you can ignore the PodDisruptionBudget requirements by setting `--ignore-pod-disruption-budget`

to `true`

. To learn more about PodDisruptionBudgets, see:

[Plan for availability using a pod disruption budget](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)[Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)[Disruptions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/)

Delete an existing node pool without following any PodDisruptionBudgets set on the cluster using the

command with the`az aks nodepool delete`

`--ignore-pod-disruption-budget`

flag set to`true`

:`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --ignore-pod-disruption-budget true`

To verify that the node pool was deleted successfully, use the

`kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Remove specific VMs in an existing node pool

Note

When you delete a VM with this command, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the VM you plan to delete, perform a cordon and drain on the VM before deleting. You can learn more about how to cordon and drain using the example scenario provided in the resizing node pools tutorial.

List the existing nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-mynodepool-20823458-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000002 Ready agent 63m v1.21.9`

Delete the specified VMs using the

command. Make sure to replace the placeholders with your own values.`az aks nodepool delete-machines`

`az aks nodepool delete-machines \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --machine-names <vm-name-1> <vm-name-2>`

Verify the VMs were successfully deleted using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should no longer include the VMs that you specified in the

`az aks nodepool delete-machines`

command.

## Next steps

For more information about adjusting node pool sizes in AKS, see [Resize node pools](resize-node-pool).


---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-container-image-management.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-container-image-management -->

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
