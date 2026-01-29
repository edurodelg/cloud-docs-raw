---
merged_at: 2026-01-29T15:23:36.569647
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-ray -->

# Configure and deploy a Ray cluster on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy a Ray cluster on Azure Kubernetes Service (AKS) using KubeRay. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

This article provides two methods to deploy the Ray cluster on AKS:

: Use the[Non-interactive deployment](#deploy-the-ray-sample-non-interactively)`deploy.sh`

script in the GitHub repository to deploy the complete Ray sample non-interactively.: Follow the manual deployment steps to deploy the Ray sample to AKS.[Manual deployment](#manually-deploy-the-ray-sample)

## Prerequisites

- Review the
[Ray cluster on AKS overview](ray-overview)to understand the components and deployment process. - An Azure subscription. If you don't have an Azure subscription, you can create a free account
[here](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The Azure CLI installed on your local machine. You can install it using the instructions in
[How to install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[Azure Kubernetes Service Preview extension](/en-us/azure/aks/draft#install-the-aks-preview-azure-cli-extension)installed. [Helm](https://helm.sh/docs/intro/install/)installed.[Terraform client tools](https://developer.hashicorp.com/terraform/install)or[OpenTofu](https://opentofu.org/)installed. This article uses Terraform, but the modules used should be compatible with OpenTofu.

## Deploy the Ray sample non-interactively

If you want to deploy the complete Ray sample non-interactively, you can use the `deploy.sh`

script in the GitHub repository ([https://github.com/Azure-Samples/aks-ray-sample](https://github.com/Azure-Samples/aks-ray-sample)). This script completes the steps outlined in the [Ray deployment process section](ray-overview#ray-deployment-process).

Clone the GitHub repo locally and change to the root of the repo using the following commands:

`git clone https://github.com/Azure-Samples/aks-ray-sample cd aks-ray-sample`

Deploy the complete sample using the following commands:

`chmod +x deploy.sh ./deploy.sh`

Once the deployment completes, review the output of the logs and the resource group in the Azure portal to see the infrastructure that was created.


## Manually deploy the Ray sample

Fashion MNIST is a dataset of Zalando's article images consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image associated with a label from ten classes. In this guide, you train a simple PyTorch model on this dataset using the Ray cluster.

### Deploy the RayJob specification

To train the model, you need to submit a Ray Job specification to the KubeRay operator running on a private AKS cluster. The Ray Job specification is a YAML file that describes the resources required to run the job, including the Docker image, the command to run, and the number of workers to use.

Looking at the Ray Job description, you might need to modify some fields to match your environment:

- The
`replicas`

field under the`workerGroupSpecs`

section in`rayClusterSpec`

specifies the number of worker pods that KubeRay schedules to the Kubernetes cluster. Each worker pod requires*3 CPUs*and*4 GB of memory*. The head pod requires*1 CPU*and*4 GB of memory*. Setting the`replicas`

field to*2*requires*8 vCPUs*in the node pool used to implement the RayCluster for the job. - The
`NUM_WORKERS`

field under`runtimeEnvYAML`

in`spec`

specifies the number of Ray actors to launch. Each Ray actor must be serviced by a worker pod in the Kubernetes cluster, so this field must be less than or equal to the`replicas`

field. In this example, we set`NUM_WORKERS`

to*2*, which matches the`replicas`

field. - The
`CPUS_PER_WORKER`

field must be set to*less than or equal the number of CPUs allocated to each worker pod minus 1*. In this example, the CPU resource request per worker pod is*3*, so`CPUS_PER_WORKER`

is set to*2*.

To summarize, you need a total of *8 vCPUs* in the node pool to run the PyTorch model training job. Since we added a taint on the system node pool so that no user pods can be scheduled on it, we must create a new node pool with at least *8 vCPUs* to host the Ray cluster.

Download the Ray Job specification file using the following command:

`curl -LO https://raw.githubusercontent.com/ray-project/kuberay/master/ray-operator/config/samples/pytorch-mnist/ray-job.pytorch-mnist.yaml`

Make any necessary modifications to the Ray Job specification file.

Launch the PyTorch model training job using the

`kubectl apply`

command.`kubectl apply -n kuberay -f ray-job.pytorch-mnist.yaml`


### Verify the RayJob deployment

Verify that you have two worker pods and one head pod running in the namespace using the

`kubectl get pods`

command.`kubectl get pods -n kuberay`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 6m15s pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 6m15s rayjob-pytorch-mnist-fc959 1/1 Running 0 5m35s rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 6m15s`

Check the status of the RayJob using the

`kubectl get`

command.`kubectl get rayjob -n kuberay`

Your output should look similar to the following example output:

`NAME JOB STATUS DEPLOYMENT STATUS START TIME END TIME AGE rayjob-pytorch-mnist RUNNING Running 2024-11-22T03:08:22Z 9m36s`

Wait until the RayJob completes. This might take a few minutes. Once the

`JOB STATUS`

is`SUCCEEDED`

, you can check the training logs. You can do this by first getting the name of the pod running the RayJob using the`kubectl get pods`

command.`kubectl get pods -n kuberay`

In the output, you should see a pod with a name that starts with

`rayjob-pytorch-mnist`

, similar to the following example output:`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 14m pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 14m rayjob-pytorch-mnist-fc959 0/1 Completed 0 13m rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 14m`

View the logs of the RayJob using the

`kubectl logs`

command. Make sure to replace`rayjob-pytorch-mnist-fc959`

with the name of the pod running your RayJob.`kubectl logs -n kuberay rayjob-pytorch-mnist-fc959`

In the output, you should see the training logs for the PyTorch model, similar to the following example output:

`2024-11-21 19:09:04,986 INFO cli.py:39 -- Job submission server address: http://rayjob-pytorch-mnist-raycluster-s7xd9-head-svc.kuberay.svc.cluster.local:8265 2024-11-21 19:09:05,712 SUCC cli.py:63 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' submitted successfully 2024-11-21 19:09:05,713 SUCC cli.py:65 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 INFO cli.py:289 -- Next steps 2024-11-21 19:09:05,713 INFO cli.py:290 -- Query the logs of the job: 2024-11-21 19:09:05,713 INFO cli.py:292 -- ray job logs rayjob-pytorch-mnist-hndpx 2024-11-21 19:09:05,713 INFO cli.py:294 -- Query the status of the job: ... View detailed results here: /home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23 To visualize your results with TensorBoard, run: `tensorboard --logdir /tmp/ray/session_2024-11-21_19-08-24_556164_1/artifacts/2024-11-21_19-11-24/TorchTrainer_2024-11-21_19-11-23/driver_artifacts` Training started with configuration: ╭─────────────────────────────────────────────────╮ │ Training config │ ├─────────────────────────────────────────────────┤ │ train_loop_config/batch_size_per_worker 16 │ │ train_loop_config/epochs 10 │ │ train_loop_config/lr 0.001 │ ╰─────────────────────────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Setting up process group for: env:// [rank=0, world_size=2] (TorchTrainer pid=1138, ip=10.244.4.193) Started distributed worker processes: (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=3ea81f12c0f73ebfbd5b46664e29ced00266e69355c699970e1d824b, ip=10.244.4.193, pid=1193) world_rank=0, local_rank=0, node_rank=0 (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=2b00ea2b369c9d27de9596ce329daad1d24626b149975cf23cd10ea3, ip=10.244.1.42, pid=1341) world_rank=1, local_rank=0, node_rank=1 (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 0.00/26.4M [00:00<?, ?B/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 65.5k/26.4M [00:00<01:13, 356kB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.9MB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Extracting /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw (RayTrainWorker pid=1341, ip=10.244.1.42) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.7MB/s] ... Training finished iteration 1 at 2024-11-21 19:15:46. Total running time: 4min 22s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 144.9 │ │ time_total_s 144.9 │ │ training_iteration 1 │ │ accuracy 0.805 │ │ loss 0.52336 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 97%|█████████▋| 303/313 [00:01<00:00, 269.60it/s] Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 267.14it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 270.44it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 0: 100%|█████████▉| 1866/1875 [00:24<00:00, 82.49it/s] [repeated 35x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 77.99it/s] Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 76.19it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 88%|████████▊ | 275/313 [00:01<00:00, 265.39it/s] [repeated 19x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 19%|█▉ | 354/1875 [00:04<00:18, 82.66it/s] [repeated 80x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 40%|████ | 757/1875 [00:09<00:13, 83.01it/s] [repeated 90x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 62%|██████▏ | 1164/1875 [00:14<00:08, 83.39it/s] [repeated 92x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 82%|████████▏ | 1533/1875 [00:19<00:05, 68.09it/s] [repeated 91x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 91%|█████████▏| 1713/1875 [00:22<00:02, 70.20it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 91%|█████████ | 1707/1875 [00:22<00:02, 70.04it/s] [repeated 47x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 8%|▊ | 24/313 [00:00<00:01, 237.98it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 96%|█████████▋| 302/313 [00:01<00:00, 250.76it/s] Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 262.94it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 2: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 92%|█████████▏| 289/313 [00:01<00:00, 222.57it/s] Training finished iteration 2 at 2024-11-21 19:16:12. Total running time: 4min 48s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 25.975 │ │ time_total_s 170.875 │ │ training_iteration 2 │ │ accuracy 0.828 │ │ loss 0.45946 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 226.04it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 100%|██████████| 1875/1875 [00:24<00:00, 76.24it/s] [repeated 45x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 2: 13%|█▎ | 239/1875 [00:03<00:24, 67.30it/s] [repeated 64x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 85%|████████▍ | 266/313 [00:01<00:00, 222.54it/s] [repeated 20x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) .. Training completed after 10 iterations at 2024-11-21 19:19:47. Total running time: 8min 23s 2024-11-21 19:19:47,596 INFO tune.py:1009 -- Wrote the latest version of all result files and experiment state to '/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23' in 0.0029s. Training result: Result( metrics={'loss': 0.35892221605786073, 'accuracy': 0.872}, path='/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23/TorchTrainer_74867_00000_0_2024-11-21_19-11-24', filesystem='local', checkpoint=None ) (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Extracting /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 91%|█████████ | 1708/1875 [00:21<00:01, 83.84it/s] [repeated 23x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 100%|██████████| 1875/1875 [00:23<00:00, 78.52it/s] [repeated 37x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 9: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 89%|████████▉ | 278/313 [00:01<00:00, 266.46it/s] [repeated 19x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 97%|█████████▋| 305/313 [00:01<00:00, 256.69it/s] Test Epoch 9: 100%|██████████| 313/313 [00:01<00:00, 267.35it/s] 2024-11-21 19:19:51,728 SUCC cli.py:63 -- ------------------------------------------ 2024-11-21 19:19:51,728 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' succeeded 2024-11-21 19:19:51,728 SUCC cli.py:65 -- ------------------------------------------`


## View training results on the Ray Dashboard

When the RayJob successfully completes, you can view the training results on the Ray Dashboard. The Ray Dashboard provides real-time monitoring and visualizations of Ray clusters. You can use the Ray Dashboard to monitor the status of Ray clusters, view logs, and visualize the results of machine learning jobs.

To access the Ray Dashboard, you need to expose the Ray head service to the public internet by creating a *service shim* to expose the Ray head service on port 80 instead of port 8265.

Note

The `deploy.sh`

described in the previous section automatically exposes the Ray head service to the public internet. The following steps are included in the `deploy.sh`

script.

Get the name of the Ray head service and save it in a shell variable using the following command:

`rayclusterhead=$(kubectl get service -n $kuberay_namespace | grep 'rayjob-pytorch-mnist-raycluster' | grep 'ClusterIP' | awk '{print $1}')`

Create the service shim to expose the Ray head service on port 80 using the

`kubectl expose service`

command.`kubectl expose service $rayclusterhead \ -n $kuberay_namespace \ --port=80 \ --target-port=8265 \ --type=NodePort \ --name=ray-dash`

Create the ingress to expose the service shim using the ingress controller using the following command:

`cat <<EOF | kubectl apply -f - apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: ray-dash namespace: kuberay annotations: nginx.ingress.kubernetes.io/rewrite-target: / spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: ray-dash port: number: 80 path: / pathType: Prefix EOF`

Get the public IP address of the ingress controller using the

`kubectl get service`

command.`kubectl get service -n app-routing-system`

In the output, you should see the public IP address of the load balancer attached to the ingress controller. Copy the public IP address and paste it into a web browser. You should see the Ray Dashboard.


## Clean up resources

To clean up the resources created in this guide, you can delete the Azure resource group that contains the AKS cluster.

## Next steps

To learn more about AI and machine learning workloads on AKS, see the following articles:

[Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)](open-ai-quickstart)[Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)](use-flyte)[Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator](ai-toolchain-operator)

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni-dynamic-ip-allocation -->

# Configure Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A drawback with the traditional CNI is the exhaustion of pod IP addresses as the AKS cluster grows, which results in the need to rebuild your entire cluster in a bigger subnet. The new dynamic IP allocation capability in Azure CNI solves this problem by allocating pod IPs from a subnet separate from the subnet hosting the AKS cluster.

It offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this new solution.

This article shows you how to use Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in AKS.

## Prerequisites

Review the

[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article.Review the

[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply.AKS Engine and DIY clusters aren't supported.

Azure CLI version

`2.37.0`

or later.If you have an existing cluster, you need to enable Container Insights for monitoring IP subnet usage. You can enable Container Insights using the

command, as shown in the following example:`az aks enable-addons`

`az aks enable-addons --addons monitoring --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME`


## Plan IP addressing

Planning your IP addressing is much simpler with this feature. Since the nodes and pods scale independently, their address spaces can also be planned separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster; nodes will request 16 IPs on startup and will request another batch of 16 any time there are <8 IPs unallocated in their allotment.

The planning of IPs for Kubernetes services and Docker bridge remain unchanged.

To view and verify the NodeNetworkConfiguration (NNC) resources responsible for these IP allocations, you can run the following command:

```
kubectl get nodenetworkconfigs -n kube-system -o wide
```


## Maximum pods per node in a cluster with Pod Subnet - Dynamic IP Allocation and enhanced subnet support

The pods per node value when using Azure CNI Pod Subnet - Dynamic IP Allocation is slightly different from the traditional CNI behavior:

| CNI | Default | Configurable at deployment |
|---|---|---|
| Traditional Azure CNI | 30 | Yes (up to 250) |
| Azure CNI Pod Subnet - Dynamic IP Allocation | 250 | Yes (up to 250) |

All other guidance related to configuring the maximum pods per node remains the same.

## Deployment parameters

The [deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS are all valid, with two exceptions:

- The
**subnet**parameter now refers to the subnet related to the cluster's nodes. - An additional parameter
**pod subnet**is used to specify the subnet whose IP addresses will be dynamically allocated to pods.

## Configure Pod Subnet - Dynamic IP Allocation and enhanced subnet support - Azure CLI

Using Pod Subnet - Dynamic IP Allocation and enhanced subnet support in your cluster is similar to the default method for configuring a cluster Azure CNI. The following example walks through creating a new virtual network with a subnet for nodes and a subnet for pods, and creating a cluster that uses Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support. Be sure to replace variables such as `$subscription`

with your own values.

Create the virtual network with two subnets.

```
RESOURCE_GROUP_NAME="myResourceGroup"
VNET_NAME="myVirtualNetwork"
LOCATION="westcentralus"
SUBNET_NAME_1="nodesubnet"
SUBNET_NAME_2="podsubnet"
# Create the resource group
az group create --name $RESOURCE_GROUP_NAME --location $LOCATION
# Create our two subnet network
az network vnet create --resource-group $RESOURCE_GROUP_NAME --location $LOCATION --name $VNET_NAME --address-prefixes 10.0.0.0/8 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_1 --address-prefixes 10.240.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_2 --address-prefixes 10.241.0.0/16 -o none
```


Create the cluster, referencing the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

and enabling the monitoring add-on.

```
CLUSTER_NAME="myAKSCluster"
SUBSCRIPTION="aaaaaaa-aaaaa-aaaaaa-aaaa"
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--location $LOCATION \
--max-pods 250 \
--node-count 2 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_1 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_2 \
--enable-addons monitoring \
--generate-ssh-keys
```


### Adding node pool

When adding node pool, reference the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

. The following example creates two new subnets that are then referenced in the creation of a new node pool:

```
SUBNET_NAME_3="node2subnet"
SUBNET_NAME_4="pod2subnet"
NODE_POOL_NAME="mynodepool"
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_3 --address-prefixes 10.242.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_4 --address-prefixes 10.243.0.0/16 -o none
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --name $NODE_POOL_NAME \
--max-pods 250 \
--node-count 2 \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_3 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_4 \
--no-wait
```


## Monitor IP subnet usage

Azure CNI provides the capability to monitor IP subnet usage. To enable IP subnet usage monitoring, follow the steps below:

### Get the YAML file

Download or grep the file named container-azm-ms-agentconfig.yaml from

[GitHub](https://raw.githubusercontent.com/microsoft/Docker-Provider/ci_prod/kubernetes/container-azm-ms-agentconfig.yaml).Find

in integrations. Set`azure_subnet_ip_usage`

`enabled`

to`true`

.Save the file.


### Get the AKS credentials

Set the variables for subscription, resource group and cluster. Consider the following as examples:

```
az account set --subscription $SUBSCRIPTION
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME
```


### Apply the config

- Open the terminal in the folder in which the downloaded
**container-azm-ms-agentconfig.yaml**file is saved. - Apply the config using the
`kubectl apply -f container-azm-ms-agentconfig.yaml`

command. This will restart the pod and after 5-10 minutes, the metrics will be visible. - View the metrics on the cluster by navigating to Workbooks on the cluster page in the Azure portal, and find the workbook named
*Subnet IP Usage*.

## Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support FAQs

**Can I assign multiple pod subnets to a cluster/node pool?**Only one subnet can be assigned to a cluster or node pool. However, multiple clusters or node pools can share a single subnet.

**Can I assign Pod subnets from a different VNet altogether?**No, the pod subnet should be from the same VNet as the cluster.

**Can some node pools in a cluster use the traditional CNI while others use the new CNI?**The entire cluster should use only one type of CNI.


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/flatcar-container-linux-for-aks -->

# Use Flatcar Container Linux for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Flatcar Container Linux for AKS, a Cloud Native Compute Foundation (CNCF) project that provides security, reliability, and cross-cloud capabilities. Flatcar Container Linux is available in preview as an OS option on AKS. You can deploy Flatcar Container Linux node pools in a new AKS cluster or add Flatcar Container Linux node pools to your existing clusters. To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

## Flatcar Container Linux for AKS benefits

Flatcar uses an immutable OS filesystem, and it eliminates configuration drift and prevents unauthorized changes, ensuring robust protection for your workloads across multiple cloud platforms. Designed for versatility, Flatcar enables cross-cloud deployment, empowering businesses to scale effortlessly and securely.

## Limitations

Flatcar Container Linux for AKS has the following limitations:

[FIPS](enable-fips-nodes)isn't supported with Flatcar Container Linux.[Trusted Launch](use-trusted-launch)isn't supported with Flatcar Container Linux.[Confidential VM sizes](use-cvm)aren't supported with Flatcar Container Linux.- The
`SecurityPatch`

[node OS upgrade channel](auto-upgrade-node-os-image)isn't supported with Flatcar Container Linux. - During preview, AKS doesn't support in-place updates with Flatcar Container Linux.
[Artifact Streaming](artifact-streaming)(preview) isn't supported with Flatcar Container Linux.[Generation 1 VMs](aks-virtual-machine-sizes)aren't supported with Flatcar Container Linux, which means you can't use VM sizes that only support Generation 1.[Pod Sandboxing (preview)](use-pod-sandboxing)isn't supported with Flatcar Container Linux.[Node auto-provisioning](node-autoprovision)isn't supported with Flatcar Container Linux.[Azure Monitor VM(SS) extension](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal#:%7E:text=Virtual%20machine%20(VM)%20extension)isn't supported.

Note

If you have an existing cluster with any of the above features enabled, you might not be able to add a node pool using Flatcar Container Linux.

## Get started with Flatcar Container Linux for AKS

To get started using the Flatcar Container Linux for AKS, see the following resources:

- Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using
[Azure CLI](learn/quick-flatcar-deploy-cli) - Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an
[ARM template](learn/quick-flatcar-deploy-arm-template) - Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool using
[Azure CLI or an ARM template](create-node-pools) - Add a Flatcar Container Linux for AKS (preview) node pool to an existing cluster using
[Azure CLI or an ARM template](create-node-pools)

## OS migrations and upgrades with Flatcar Container Linux

AKS doesn't support in-place migrations from existing Linux clusters or node pools to Flatcar Container Linux clusters or node pools. To migrate existing workloads to Flatcar Container Linux for AKS, you need to recreate your node pools using `--os-sku flatcar`

.

Flatcar Container Linux for AKS releases weekly AKS node images. Versioning follows the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For example:```
az aks nodepool list --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --query '[].{name: name, nodeImageVersion: nodeImageVersion}'
```


Example output:

```
[
{
"name": "nodes",
"nodeImageVersion": "AKSFlatcar-flatcargen2-202508.06.0"
}
]
```


You can check the Flatcar version number (for example: Flatcar 4372.0.1) in the release notes and by using `kubectl get nodes`

command. For example:

```
kubectl get nodes -o wide
```


Example output:

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodes-16363508-vmss000000 Ready <none> 2m33s v1.32.6 10.224.0.4 <none> Flatcar Container Linux by Kinvolk 4372.0.1 (Oklo) 6.12.35-flatcar containerd://2.0.4
```


Flatcar's inbuilt automatic A/B update for the OS partition is disabled and only full node image updates are supported.

## Next steps

To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-observability -->

# Observability for Azure Kubernetes Service (AKS) clusters with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to view observability metrics and improve observability for AKS clusters with KMS etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - You must enable
[diagnostic settings for the key vault to check the encryption logs](/en-us/azure/key-vault/general/howto-logging).

## Check the KMS config

Get the KMS config using the

command.`az aks show`

`az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "securityProfile.azureKeyVaultKms"`

The output looks similar to the following example output:

`... "securityProfile": { "azureKeyVaultKms": { "enabled": true, "keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>/<key-id>", "keyVaultNetworkAccess": "Public", "keyVaultResourceId": <key-vault-resource-id> ...`


## Diagnose and solve problems

Because the KMS plugin is a sidecar of `kube-apiserver`

pod, you can't access it directly. To improve the observability of KMS, you can check the KMS status using the Azure portal.

- In the Azure portal, navigate to your AKS cluster.
- From the service menu, select
**Diagnose and solve problems**. - In the search bar, search for
**KMS**and select**Azure KeyVault KMS Integration Issues**.

### Example problem

Let's say you see the following issue: `KeyExpired: Operation encrypt isn't allowed on an expired key`

.

Because the AKS KMS plugin currently only allows bring your own (BYO) key vault and key, it's your responsibility to manage the key lifecycle. If the key is expired, the KMS plugin fails to decrypt the existing secrets. To resolve this issue, you need to *extend the key expiration date* to make KMS work and *rotate the key version*.

## Next steps

For more information on using KMS with AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-attach-azure-container-registry -->

# Attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code.

## Prerequisites

Before you begin, make sure you have the following resources:

- An Azure container registry. If you don't have one, create one using the steps in
[Quickstart: Create a private container registry](/en-us/azure/container-registry/container-registry-get-started-azure-cli). - An AKS cluster. If you don't have one, create one using the steps in
[Quickstart: Deploy an AKS cluster](learn/quick-kubernetes-deploy-cli). - The Azure Kubernetes Service (AKS) extension for Visual Studio Code downloaded. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation).

## Attach your Azure container registry to your AKS cluster

You can access the screen for attaching your container registry to your AKS cluster using the command palette or the Kubernetes view.

On your keyboard, press

`Ctrl+Shift+P`

to open the command palette.Enter the following information:

**Subscription**: Select the Azure subscription that holds your resources.**ACR Resource Group**: Select the resource group for your container registry.**Container Registry**: Select the container registry you want to attach to your cluster.**Cluster Resource Group**: Select the resource group for your cluster.**Cluster**: Select the cluster you want to attach to your container registry.

Select

**Attach**.You should see a green checkmark, which means your container registry is attached to your AKS cluster.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-upgrade-cluster -->

# Tutorial - Upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As part of the application and cluster lifecycle, you might want to upgrade to the latest available version of Kubernetes. You can upgrade your Azure Kubernetes Service (AKS) cluster using the Azure CLI, Azure PowerShell, or the Azure portal.

In this tutorial, you upgrade an AKS cluster. You learn how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

## Before you begin

In previous tutorials, you packaged an application into a container image and uploaded the container image to Azure Container Registry (ACR). You also created an AKS cluster and deployed an application to it. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

If using Azure CLI, this tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

If using Azure PowerShell, this tutorial requires Azure PowerShell version 5.9.0 or later. Run `Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see [Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).

## Get available cluster versions

Before you upgrade, check which Kubernetes releases are available for your cluster using the

command.`az aks get-upgrades`

`az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster`

The following example output shows the current version as

*1.28.9*and lists the available versions under`upgrades`

:`{ "agentPoolProfiles": null, "controlPlaneProfile": { "kubernetesVersion": "1.28.9", ... "upgrades": [ { "isPreview": null, "kubernetesVersion": "1.29.4" }, { "isPreview": null, "kubernetesVersion": "1.29.2" } ] }, ... }`


## Upgrade an AKS cluster

AKS nodes are carefully cordoned and drained to minimize any potential disruptions to running applications. During this process, AKS performs the following steps:

- Adds a new buffer node (or as many nodes as configured in
[max surge](upgrade-aks-cluster#customize-node-surge-upgrade)) to the cluster that runs the specified Kubernetes version. [Cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)one of the old nodes to minimize disruption to running applications. If you're using max surge, it[cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)as many nodes at the same time as the number of buffer nodes specified.- When the old node is fully drained, it's reimaged to receive the new version and becomes the buffer node for the following node to be upgraded.
- This process repeats until all nodes in the cluster have been upgraded.
- At the end of the process, the last buffer node is deleted, maintaining the existing agent node count and zone balance.

Note

If no patch is specified, the cluster automatically upgrades to the specified minor version's latest GA patch. For example, setting `--kubernetes-version`

to `1.28`

results in the cluster upgrading to `1.28.9`

.

For more information, see [Supported Kubernetes minor version upgrades in AKS](supported-kubernetes-versions#alias-minor-version).

You can either [manually upgrade your cluster](#manually-upgrade-cluster) or [configure automatic cluster upgrades](#configure-automatic-cluster-upgrades). **We recommend you configure automatic cluster upgrades to ensure your cluster is always running the latest version of Kubernetes**.

### Manually upgrade cluster

Upgrade your cluster using the

command.`az aks upgrade`

`az aks upgrade \ --resource-group myResourceGroup \ --name myAKSCluster \ --kubernetes-version KUBERNETES_VERSION`

You will be prompted to confirm the upgrade operation, and to confirm that you want to upgrade the control plane

*and*all the node pools to the selected version of Kubernetes:`Are you sure you want to perform this operation? (y/N): y Since control-plane-only argument is not specified, this will upgrade the control plane AND all nodepools to version 1.29.2. Continue? (y/N): y`

Note

You can only upgrade one minor version at a time. For example, you can upgrade from

*1.14.x*to*1.15.x*, but you can't upgrade from*1.14.x*to*1.16.x*directly. To upgrade from*1.14.x*to*1.16.x*, you must first upgrade from*1.14.x*to*1.15.x*, then perform another upgrade from*1.15.x*to*1.16.x*.The following example output shows the result of upgrading to

*1.29.2*. Notice the`kubernetesVersion`

now shows*1.29.2*:`{ ... "agentPoolProfiles": [ { ... "count": 3, "currentOrchestratorVersion": "1.29.2", "maxPods": 110, "name": "nodepool1", "nodeImageVersion": "AKSUbuntu-2204gen2containerd-202405.27.0", "orchestratorVersion": "1.29.2", "osType": "Linux", "upgradeSettings": { "drainTimeoutInMinutes": null, "maxSurge": "10%", "nodeSoakDurationInMinutes": null, "undrainableNodeBehavior": null }, "vmSize": "Standard_DS2_v2", ... } ], ... "currentKubernetesVersion": "1.29.2", "dnsPrefix": "myAKSClust-myResourceGroup-19da35", "enableRbac": false, "fqdn": "myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io", "id": "/subscriptions/<Subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster", "kubernetesVersion": "1.29.2", "location": "westus2", "name": "myAKSCluster", "type": "Microsoft.ContainerService/ManagedClusters" ... }`


### Configure automatic cluster upgrades

Set an auto-upgrade channel on your cluster using the

command with the`az aks update`

`--auto-upgrade-channel`

parameter set to`patch`

.`az aks update --resource-group myResourceGroup --name myAKSCluster --auto-upgrade-channel patch`


For more information, see [Automatically upgrade an Azure Kubernetes Service (AKS) cluster](auto-upgrade-cluster).

#### Upgrade AKS node images

AKS regularly provides new node images. Linux node images are updated weekly, and Windows node images are updated monthly. We recommend upgrading your node images frequently to use the latest AKS features and security updates. For more information, see [Upgrade node images in Azure Kubernetes Service (AKS)](node-image-upgrade). To configure automatic node image upgrades, see [Automatically upgrade Azure Kubernetes Service (AKS) cluster node operating system images](auto-upgrade-node-image).

## View the upgrade events

Note

When you upgrade your cluster, the following Kubernetes events might occur on the nodes:

**Surge**: Create a surge node.**Drain**: Evict pods from the node. Each pod has a*five minute timeout*to complete the eviction.**Update**: Update of a node has succeeded or failed.**Delete**: Delete a surge node.

View the upgrade events in the default namespaces using the

`kubectl get events`

command.`kubectl get events --field-selector source=upgrader`

The following example output shows some of the above events listed during an upgrade:

`LAST SEEN TYPE REASON OBJECT MESSAGE ... 5m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 5m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Deleting node aks-nodepool1-96663640-vmss000000 from API server 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully reimaged node: aks-nodepool1-96663640-vmss000000 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully upgraded node: aks-nodepool1-96663640-vmss000000 4m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 ...`


## Validate an upgrade

Confirm the upgrade was successful using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --output table`

The following example output shows the AKS cluster runs

*KubernetesVersion 1.27.3*:`Name Location ResourceGroup KubernetesVersion CurrentKubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------------ ------------------- ---------------------------------------------------------------- myAKSCluster westus2 myResourceGroup 1.29.2 1.29.2 Succeeded myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io`


## Delete the cluster

As this tutorial is the last part of the series, you might want to delete your AKS cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal). If you used a managed identity, the identity is managed by the platform and doesn't require that you provision or rotate any secrets.

## Next steps

In this tutorial, you upgraded Kubernetes in an AKS cluster. You learned how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

For more information on AKS, see the [AKS overview](intro-kubernetes). For guidance on how to create full solutions with AKS, see the [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?WT.mc_id=AKSDOCSPAGE).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-azure-ad -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-authentication-microsoft-entra-id -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster -->

# Automatically upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Part of the AKS cluster lifecycle involves performing periodic upgrades to the latest Kubernetes version. It's important you apply the latest security releases or upgrade to get the latest features. Before you learn about automatic upgrades, make sure you understand the [AKS cluster upgrade fundamentals](upgrade-cluster).

Note

Any upgrade operation, whether performed manually or automatically, upgrades the node image version if it's not already on the latest version. The latest version is contingent on a full AKS release and can be determined by visiting the [AKS release tracker](release-tracker).

Autoupgrade first upgrades the control plane, and then upgrades agent pools one by one.

## Why use cluster autoupgrade

Cluster autoupgrade provides a *set once and forget* mechanism that yields tangible time and operational cost benefits. You don't need to stop your workloads, redeploy your workloads, or create a new AKS cluster. By enabling autoupgrade, you can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes.

AKS follows a strict supportability versioning window. With properly selected autoupgrade channels, you can avoid clusters falling into an unsupported version. For more on the AKS support window, see [Alias minor versions](supported-kubernetes-versions).

## Customer versus AKS-initiated autoupgrades

You can specify cluster autoupgrade specifics using the following guidance. The upgrades occur based on your specified cadence and are recommended to remain on supported Kubernetes versions.

AKS also initiates autoupgrades for unsupported clusters. When a cluster in an n-3 version (where n is the latest supported AKS GA minor version) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support [policy](supported-kubernetes-versions). Automatically upgrading a platform supported cluster to a supported version is enabled by default. Stopped node pools are upgraded during an autoupgrade operation. The upgrade applies to nodes when the node pool is started. To minimize disruptions, set up [maintenance windows](planned-maintenance).

## Cluster autoupgrade limitations

If you're using cluster autoupgrade, you can no longer upgrade the control plane first, and then upgrade the individual node pools. Cluster autoupgrade always upgrades the control plane and the node pools together. You can't upgrade the control plane only. Running the `az aks upgrade --control-plane-only`

command raises the following error:

```
NotAllAgentPoolOrchestratorVersionSpecifiedAndUnchanged: Using managed cluster api, all Agent pools' OrchestratorVersion must be all specified or all unspecified. If all specified, they must be stay unchanged or the same with control plane.
```


If using the `node-image`

(legacy and not to be used) cluster autoupgrade channel or the `NodeImage`

node image autoupgrade channel, Linux [unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates) are disabled by default.

## Cluster autoupgrade channels

Automatically completed upgrades are functionally the same as manual upgrades. The [selected autoupgrade channel](planned-maintenance) determines the timing of upgrades. When making changes to autoupgrade, allow 24 hours for the changes to take effect. Automatically upgrading a cluster follows the same process as manually upgrading a cluster. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

The following upgrade channels are available:

| Channel | Action | Example |
|---|---|---|
`none` |
disables autoupgrades and keeps the cluster at its current version of Kubernetes. | Default setting if left unchanged. |
`patch` |
automatically upgrades the cluster to the latest supported patch version when it becomes available while keeping the minor version the same. | For example, if a cluster runs version 1.17.7, and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.17.9. |
`stable` |
automatically upgrades the cluster to the latest supported patch release on minor version N-1, where N is the latest supported minor version. |
For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.18.6. |
`rapid` |
automatically upgrades the cluster to the latest supported patch release on the latest supported minor version. | In cases where the cluster's Kubernetes version is an N-2 minor version, where N is the latest supported minor version, the cluster first upgrades to the latest supported patch version on N-1 minor version. For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster first upgrades to 1.18.6, then upgrades to 1.19.1. |
`node-image` (legacy) |
automatically upgrades the node image to the latest version available. | Microsoft provides patches and new images for image nodes frequently (weekly), but your running nodes don't get the new images unless you do a node image upgrade. Turning on the node-image channel automatically updates your node images whenever a new version is available. If you use this channel, Linux [unattended upgrades] are disabled by default. Node image upgrades work on patch versions that are deprecated, so long as the minor Kubernetes version is still supported. This channel is no longer recommended and is planned for deprecation in future. For an option that can automatically upgrade node images, see the `NodeImage` channel in
|

Note

Keep the following information in mind when using cluster autoupgrade:

Cluster autoupgrade only updates to GA versions of Kubernetes and doesn't update to preview versions.

With AKS, you can create a cluster without specifying the exact patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. To learn more, see

[AKS support window](supported-kubernetes-versions).Autoupgrade requires the cluster's Kubernetes version to be within the

[AKS support window](supported-kubernetes-versions), even if using the`node-image`

channel.If you're using the preview API

`11-02-preview`

or later, and you select the`node-image`

cluster autoupgrade channel, the[node image autoupgrade channel](auto-upgrade-node-image)automatically sets to`NodeImage`

.Each cluster can only be associated with a single autoupgrade channel. The reason is because your specified channel determines the Kubernetes version that runs on the cluster.

If your cluster has no autoupgrade channel and you enable it for Long-Term Support (LTS), the cluster defaults to a

`patch`

autoupgrade channel.

## Use cluster autoupgrade with a new AKS cluster

Set the autoupgrade channel when creating a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and the

`auto-upgrade-channel`

parameter.```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster"
az aks create --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable --generate-ssh-keys
```


## Use cluster autoupgrade with an existing AKS cluster

Set the autoupgrade channel on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`auto-upgrade-channel`

parameter.```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable
```


Results:

```
{
"id": "/subscriptions/aaaa6a6a-bb7b-cc8c-dd9d-eeeeee0e0e0e/resourceGroups/myResourceGroupabc123/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
"properties": {
"autoUpgradeChannel": "stable",
"provisioningState": "Succeeded"
}
}
```


## Use autoupgrade with Planned Maintenance

If using Planned Maintenance and cluster autoupgrade, your upgrade starts during your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of *four hours or more*.

For more information on how to set a maintenance window with Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Best practices for cluster autoupgrade

Use the following best practices to help maximize your success when using autoupgrade:

- To ensure your cluster is always in a supported version, for example within the N-2 rule, choose either
`stable`

or`rapid`

channels. - If you're interested in getting the latest patches as soon as possible, use the
`patch`

channel. The`node-image`

channel is a good fit if you want your agent pools to always run the most recent node images. - To automatically upgrade node images while using a different cluster upgrade channel, consider using the
[node image autoupgrade](auto-upgrade-node-image)`NodeImage`

channel. - Follow
[Operator best practices](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets). - Follow
[PodDisruptionBudget (PDB) best practices](https://kubernetes.io/docs/tasks/run-application/configure-pdb/). - For upgrade troubleshooting information, see the
[AKS troubleshooting documentation](/en-us/support/azure/azure-kubernetes/welcome-azure-kubernetes).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-tool-calling -->

# Integrate tool calling with LLM Inference with the AI toolchain operator add-on on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS) with support for OpenAI-style tool calling. You also learn how to validate tool calling functionality using vLLM metrics and local function mocks.

## What is tool calling?

Tool calling enables large language models (LLMs) to interface with external functions, APIs, or services. Instead of just generating text, an LLM can decide:

- "I need to call a weather API."
- "I need to use a calculator."
- "I should search a database."

It does this by invoking a defined “tool” with parameters it chooses based on the user’s request. Tool calling is useful for:

- Chatbots that book, summarize, or calculate.
- Enterprise LLM applications where hallucination must be minimized.
- Agent frameworks (AutoGen, LangGraph, LangChain, AgentOps, etc.).

In production environments, AI-enabled applications often demand more than natural language generation; they require the ability to take action based on user intent. Tool calling empowers LLMs to extend beyond text responses by invoking external tools, APIs, or custom logic in real time. This bridges the gap between language understanding and execution, enabling developers to build interactive AI assistants, agents, and automation workflows that are both accurate and useful. Instead of relying on static responses, LLMs can now access live data, trigger services, and complete tasks on behalf of users, both safely and reliably.

When deployed on AKS, tool calling becomes scalable, secure, and production ready. Kubernetes provides the flexibility to orchestrate inference workloads using high-performance runtimes like vLLM, while ensuring observability and governance of tool usage. With this pattern, AKS operators and app developers can more seamlessly update models or tools independently and deploy advanced AI features without compromising reliability.

As a result, tool calling on AKS is now a foundational pattern for building modern AI apps that are context-aware, action-capable, and enterprise-ready.

### Tool calling with KAITO

To streamline this deployment model, the AI toolchain operator (KAITO) add-on for AKS provides a managed solution for running inference services with [tool calling support](https://kaito-project.github.io/kaito/docs/tool-calling/). By leveraging KAITO inference workspaces, you can quickly spin up scalable, GPU-accelerated model endpoints with built-in support for tool calling and OpenAI-compatible APIs. This eliminates the operational overhead of configuring runtimes, managing dependencies, or scaling infrastructure manually.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster. - A deployed KAITO inference workspace that supports tool calling. Refer to the official
[KAITO tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/)documentation for the tool calling supported models with vLLM. - You deployed the
`workspace‑phi‑4-mini-toolcall`

[KAITO workspace](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_tool_calling.yaml)with the default configuration.

## Confirm the KAITO inference workspace is running

Monitor your workspace deployment with the

`kubectl get`

command.`kubectl get workspace workspace‑phi‑4‑mini-toolcall -w`

In the output, you want to verify the resource (

`ResourceReady`

) and inference (`InferenceReady`

) are ready and the workspace succeeded (`WorkspaceSucceeded`

being`true`

).

## Confirm the inference API is ready to serve

Once the

[workspace is ready](#confirm-the-kaito-inference-workspace-is-running), find the service endpoint using the`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check the

`/v1/models`

endpoint to confirm the LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

To ensure the LLM is deployed, and the API is working, your output should be similar to the following:

`... { "object": "list", "data": [ { "id": "phi‑4‑mini‑instruct", ... ... } ] } ...`


## Test the named function tool‐calling

In this example, the `workspace‑phi‑4‑mini-toolcall`

workspace supports named function tool-calling by default, so we can confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure.

The Python snippet we use in this section is from the [KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/#examples) and uses an OpenAI‑compatible client.

Confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure. This example:

- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at
`http://localhost:8000/v1`

and accepts OpenAI-style API calls. - Simulates the backend logic for a tool called
`get_weather`

. (In a real scenario, this would call a weather API.) - Describes the tool interface; the
`Phi-4-mini`

LLM will see this tool and decide whether to use it based on the user's input. - Sends a sample chat message to the model and provides the tool spec. The setting
`tool_choice="auto"`

allows the LLM to decide if it should call a tool based on the prompt. - In this case, the user's request was relevant to the
`get_weather`

tool, so we simulate the execution of the tool, calling the local function with the model's chosen arguments.

`from openai import OpenAI import json # local server client = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy") def get_weather(location: str, unit: str) -> str: return f"Getting the weather for {location} in {unit}..." tool_functions = {"get_weather": get_weather} tools = [{ "type": "function", "function": { "name": "get_weather", "description": "Get the current weather in a given location", "parameters": { "type": "object", "properties": { "location": {"type": "string"}, "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]} }, "required": ["location", "unit"] } } }] response = client.chat.completions.create( model="phi‑4‑mini‑instruct", # or client.models.list().data[0].id messages=[{"role": "user", "content": "What's the weather like in San Francisco?"}], tools=tools, tool_choice="auto" ) # Inspect response tool_call = response.choices[0].message.tool_calls[0].function args = json.loads(tool_call.arguments) print("Function called:", tool_call.name) print("Arguments:", args) print("Result:", tool_functions[tool_call.name](**args))`

Your output should look similar to the following:

`Function called: get_weather Arguments: {"location": "San Francisco, CA", "unit": "fahrenheit"} Result: Getting the weather for San Francisco, CA in fahrenheit...`

The “tool_calls” field comes back, meaning the

`Phi-4-mini`

LLM decided to invoke the function. Now, a sample tool call has been successfully parsed and executed based on the model’s decision to confirm end-to-end tool calling behavior with the KAITO inference deployment.- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at

## Troubleshooting

### Model preset doesn’t support tool calling

If you pick a model that isn't on the supported list, tool calling might not work. Make sure you [review the KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/), which explicitly lists which presets support tool calling.

### Misaligned runtime

The KAITO inference must use [vLLM runtime for tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/#supported-inference-runtimes) (HuggingFace Transformers runtime generally doesn’t support tool calling in KAITO).

### Network / endpoint issues

If port-forwarding, ensure the service ports are correctly forwarded. If the external MCP server is unreachable, will error out.

### Timeouts

External MCP server calls might take time. Make sure the adapter or client timeout is sufficiently high.

### Authentication

If the external MCP server requires authentication (API key, header, etc.), ensure you supply correct credentials.

## Next steps

- Set up
[vLLM monitoring in the AI toolchain operator add-on](ai-toolchain-operator-monitoring)with Prometheus and Grafana on AKS. - Learn about
[MCP server support with KAITO](ai-toolchain-operator-mcp)and test standardized tool calling examples on your AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-telemetry -->

# Telemetry API for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Istio can [generate metrics, distributed traces, and access logs](https://istio.io/latest/docs/concepts/observability/) for all workloads in the mesh. The Istio-based service mesh add-on for Azure Kubernetes Service (AKS) provides telemetry customization options through the [shared MeshConfig](istio-meshconfig) and the Istio Telemetry API `v1`

for Istio add-on minor revisions `asm-1-22`

and higher.

Note

While the [Istio MeshConfig](istio-meshconfig) also provides options for configuring telemetry globally across the mesh, the Telemetry API offers more granular control over telemetry settings on a per-service or per-workload basis. As the Istio community continues to invest in the Telemetry API, it is now the preferred method for telemetry configuration. We encourage migrating to the Telemetry API for configuring telemetry to be collected in the mesh.

## Prerequisites

- You must be on revision
`asm-1-22`

or higher. For information on how to perform minor version upgrades, see the[Istio add-on upgrade documentation](istio-upgrade).

## Configure Telemetry resources

The following example demonstrates how Envoy access logging can be enabled across the mesh for the Istio add-on via the Telemetry API using `asm-1-22`

(adjust the revision as needed). For guidance on other Telemetry API customizations for the add-on, see the [Telemetry API support scope](#telemetry-api-support-scope) section and the [Istio documentation](https://istio.io/latest/docs/reference/config/telemetry/).

### Deploy sample applications

Label the namespace for sidecar injection:

```
kubectl label ns default istio.io/rev=asm-1-22
```


Deploy the `sleep`

application and set the `SOURCE_POD`

environment variable:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/sleep/sleep.yaml
export SOURCE_POD=$(kubectl get pod -l app=sleep -o jsonpath={.items..metadata.name})
```


Then, deploy the `httpbin`

application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/httpbin/httpbin.yaml
```


### Enable Envoy access logging with the Istio Telemetry API

Deploy the following Istio `v1`

Telemetry API resource to enable Envoy access logging for the entire mesh:

```
cat <<EOF | kubectl apply -n aks-istio-system -f -
apiVersion: telemetry.istio.io/v1
kind: Telemetry
metadata:
name: mesh-logging-default
spec:
accessLogging:
- providers:
- name: envoy
EOF
```


### Test access logs

Send a request from `sleep`

to `httpbin`

:

```
kubectl exec "$SOURCE_POD" -c sleep -- curl -sS -v httpbin:8000/status/418
```


Verify that access logs are visible for the `sleep`

pod:

```
kubectl logs -l app=sleep -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.690Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 12 11 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" outbound|8000||httpbin.default.svc.cluster.local 10.244.0.12:53336 10.0.112.220:8000 10.244.0.12:42360 - default
```


Now, verify that access logs are visible for the `httpbin`

pod:

```
kubectl logs -l app=httpbin -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.696Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 2 1 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" inbound|8080|| 127.0.0.6:55401 10.244.0.13:8080 10.244.0.12:53336 outbound_.8000_._.httpbin.default.svc.cluster.local default
```


## Telemetry API support scope

For the Istio service mesh add-on for AKS, Telemetry API fields are classified as `allowed`

, `supported`

, and `blocked`

values. For more information about the Istio add-on's support policy for features and mesh configurations, see the Istio add-on [support policy document](istio-support-policy#allowed-supported-and-blocked-customizations).

The following Telemetry API configurations are either `allowed`

or `supported`

for the Istio add-on. Any field not included in this table is `blocked`

.

Telemetry API Field |
Supported/Allowed |
Notes |
|---|---|---|
`accessLogging.match` |
Supported | - |
`accessLogging.disabled` |
Supported | - |
`accessLogging.providers` |
Allowed | The default `envoy` access log provider is supported. For a managed experience for log collection and querying, see
`allowed` but unsupported. |
`metrics.overrides` |
Supported | - |
`metrics.providers` |
Allowed | Metrics collection with
`allowed` but unsupported. |

`tracing.*`

`allowed`

but unsupported.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-scenarios-hub -->

# AKS upgrade scenarios: Choose your path

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrading Azure Kubernetes Service (AKS) clusters safely requires the right strategy for your specific situation. Use this hub to quickly identify your scenario and get targeted guidance.

## What this article covers

This decision hub helps you choose the right AKS upgrade approach based on:

- A quick scenario finder with time constraints and priorities.
- Emergency upgrade paths for critical security responses.
- A strategy matrix that compares downtime tolerance and complexity.
- Role-based guidance for site reliability engineers, database administrators, developers, and security teams.
- Decision trees for complex multi-environment setups.

This hub is best for first-time upgraders, teams that need to evaluate options, and complex environments that require tailored approaches.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-aks-cluster).

## Quick scenario finder

What's your primary concern? Select your answer from the following table.

| My priority | Time constraint | Go to |
|---|---|---|
| Zero production downtime | Upgrade needed within hours |
|

[Staged fleet upgrades](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)[Safe version intake](aks-production-upgrade-strategies#scenario-3-safe-kubernetes-version-intake)[Fast security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)[Stateful workload patterns](stateful-workload-upgrades)[Seamless architecture](aks-production-upgrade-strategies#scenario-5-application-architecture-for-seamless-upgrades)## Emergency upgrade (30-90 minutes)

If you need a critical security patch now, select a link for instructions:

**Immediate action:**[Automated security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)**With stateful workloads:**[Database safety patterns](stateful-workload-upgrades#emergency-upgrade-checklist)**Rollback ready:**[Quick recovery guide](aks-production-upgrade-strategies#emergency-rollback-procedures)

## Upgrade strategy matrix

Find your ideal approach based on business constraints.

| Downtime tolerance | Environment | Best strategy | Time investment |
|---|---|---|---|
| <2 minutes | Production | Blue-green deployment | 45-60 min |
| <30 seconds | Stateful apps | Ferris wheel pattern | 60-90 min |
| Planned window | Multi-environment | Staged fleet upgrade | 2-4 hours |
| Zero tolerance | Mission-critical | Application architecture | Ongoing |

## Key upgrade topics

### Core upgrade mechanics

### Production-ready strategies

[Scenario-based production upgrades](aks-production-upgrade-strategies)[Stateful workload upgrade patterns](stateful-workload-upgrades)[Cross-environment upgrade staging](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)

### Advanced topics

## Quick wins (5-15 minutes)

Immediate actions that you can take:

**Pre-upgrade health check:**Run[cluster diagnostics](aks-diagnostics).**Backup validation:**Verify your[disaster recovery](ha-dr-overview)setup.**Monitoring setup:**Enable[upgrade notifications](aks-communication-manager).**Team preparation:**Review[support policies](support-policies).

## Learning path

If you're new to AKS upgrades, follow this learning sequence:

**Learn:**Learn about[Kubernetes concepts](core-aks-concepts)and read the[Upgrade overview](upgrade-cluster).**Practice:**Take the tutorial on how to[upgrade an AKS cluster](tutorial-kubernetes-upgrade-cluster).**Production:**Use the[production strategies](aks-production-upgrade-strategies).**Optimize:**Find out about[stateful patterns](stateful-workload-upgrades).

## Pro tips

**Always test in nonproduction first:**Perform tests even for emergency patches.**Monitor during upgrades:**Set up[real-time alerts](aks-communication-manager).**Plan for rollback:**Have a tested recovery procedure.**Communicate with teams:**Coordinate with app owners during upgrades.

## Related content

- For more help, choose your scenario from the preceding options or start with
[Production upgrade strategies](aks-production-upgrade-strategies). - For more information, see
[AKS support options](aks-support-help)or the[Troubleshooting guide](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-postgresql-ha -->

# Create infrastructure for deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create the infrastructure resources needed to deploy a highly available PostgreSQL database on AKS using the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- Review the deployment overview and make sure you meet all the prerequisites in
[How to deploy a highly available PostgreSQL database on AKS with Azure CLI](postgresql-ha-overview). [Set environment variables](#set-environment-variables)for use throughout this guide.[Install the required extensions](#install-required-extensions).

## Set environment variables

Set the following environment variables for use throughout this guide:

```
export SUFFIX=$(cat /dev/urandom | LC_ALL=C tr -dc 'a-z0-9' | fold -w 8 | head -n 1)
export LOCAL_NAME="cnpg"
export TAGS="owner=user"
export RESOURCE_GROUP_NAME="rg-${LOCAL_NAME}-${SUFFIX}"
export PRIMARY_CLUSTER_REGION="canadacentral"
export AKS_PRIMARY_CLUSTER_NAME="aks-primary-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_MANAGED_RG_NAME="rg-${LOCAL_NAME}-primary-aksmanaged-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME="pg-primary-fedcred1-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_PG_DNSPREFIX=$(echo $(echo "a$(openssl rand -hex 5 | cut -c1-11)"))
export AKS_UAMI_CLUSTER_IDENTITY_NAME="mi-aks-${LOCAL_NAME}-${SUFFIX}"
export AKS_CLUSTER_VERSION="1.32"
export PG_NAMESPACE="cnpg-database"
export PG_SYSTEM_NAMESPACE="cnpg-system"
export PG_PRIMARY_CLUSTER_NAME="pg-primary-${LOCAL_NAME}-${SUFFIX}"
export PG_PRIMARY_STORAGE_ACCOUNT_NAME="hacnpgpsa${SUFFIX}"
export PG_STORAGE_BACKUP_CONTAINER_NAME="backups"
export MY_PUBLIC_CLIENT_IP=$(dig +short myip.opendns.com @resolver3.opendns.com)
```


## Install required extensions

Install the extensions needed for Kubernetes integration and monitoring:

```
az extension add --upgrade --name k8s-extension --yes
az extension add --upgrade --name amg --yes
```


As a prerequisite for using `kubectl`

, you need to first install [Krew](https://krew.sigs.k8s.io/), followed by the installation of the [CNPG plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). These installations enable the management of the PostgreSQL operator using the subsequent commands.

```
(
set -x; cd "$(mktemp -d)" &&
OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
KREW="krew-${OS}_${ARCH}" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
tar zxvf "${KREW}.tar.gz" &&
./"${KREW}" install krew
)
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
kubectl krew install cnpg
```


## Create a resource group

Create a resource group to hold the resources you create in this guide using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create \
--name $RESOURCE_GROUP_NAME \
--location $PRIMARY_CLUSTER_REGION \
--tags $TAGS \
--query 'properties.provisioningState' \
--output tsv
```


## Create a user-assigned managed identity

In this section, you create a user-assigned managed identity (UAMI) to allow the CNPG PostgreSQL to use an AKS workload identity to access Azure Blob Storage. This configuration allows the PostgreSQL cluster on AKS to connect to Azure Blob Storage without a secret.

Create a user-assigned managed identity using the

command.`az identity create`

`AKS_UAMI_WI_IDENTITY=$(az identity create \ --name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --output json)`

Enable AKS workload identity and generate a service account to use later in this guide using the following commands:

`export AKS_UAMI_WORKLOAD_OBJECTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.principalId') export AKS_UAMI_WORKLOAD_RESOURCEID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.id') export AKS_UAMI_WORKLOAD_CLIENTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.clientId') echo "ObjectId: $AKS_UAMI_WORKLOAD_OBJECTID" echo "ResourceId: $AKS_UAMI_WORKLOAD_RESOURCEID" echo "ClientId: $AKS_UAMI_WORKLOAD_CLIENTID"`


The object ID is a unique identifier for the client ID (also known as the application ID) that uniquely identifies a security principal of type *Application* within the Microsoft Entra ID tenant. The resource ID is a unique identifier to manage and locate a resource in Azure. These values are required to enabled AKS workload identity.

The CNPG operator automatically generates a service account called *postgres* that you use later in the guide to create a federated credential that enables OAuth access from PostgreSQL to Azure Storage.

## Create a storage account in the primary region

Create an object storage account to store PostgreSQL backups in the primary region using the

command.`az storage account create`

`az storage account create \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard_ZRS \ --kind StorageV2 \ --query 'provisioningState' \ --output tsv`

Create the storage container to store the Write Ahead Logs (WAL) and regular PostgreSQL on-demand and scheduled backups using the

command.`az storage container create`

`az storage container create \ --name $PG_STORAGE_BACKUP_CONTAINER_NAME \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --auth-mode login`

Example output:

`{ "created": true }`

Note

If you encounter the error message:

`The request may be blocked by network rules of storage account. Please check network rule set using 'az storage account show -n accountname --query networkRuleSet'. If you want to change the default action to apply when no rule matches, please use 'az storage account update'`

. Make sure to verify user permissions for Azure Blob Storage and, if**necessary**, elevate your role to`Storage Blob Data Owner`

using the commands provided and after retry thecommand.`az storage container create`

`export USER_ID=$(az ad signed-in-user show --query id --output tsv) export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) az role assignment list --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID --output table az role assignment create \ --assignee-object-id $USER_ID \ --assignee-principal-type User \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --role "Storage Blob Data Owner" \ --output tsv`


## Assign RBAC to storage accounts

To enable backups, the PostgreSQL cluster needs to read and write to an object store. The PostgreSQL cluster running on AKS uses a workload identity to access the storage account via the CNPG operator configuration parameter [ inheritFromAzureAD](https://cloudnative-pg.io/documentation/1.23/appendixes/object_stores/#azure-blob-storage).

Get the primary resource ID for the storage account using the

command.`az storage account show`

`export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) echo $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID`

Assign the "Storage Blob Data Contributor" Azure built-in role to the object ID with the storage account resource ID scope for the UAMI associated with the managed identity for each AKS cluster using the

command.`az role assignment create`

`az role assignment create \ --role "Storage Blob Data Contributor" \ --assignee-object-id $AKS_UAMI_WORKLOAD_OBJECTID \ --assignee-principal-type ServicePrincipal \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --query "id" \ --output tsv`


## Set up monitoring infrastructure

In this section, you deploy an instance of Azure Managed Grafana, an Azure Monitor workspace, and an Azure Monitor Log Analytics workspace to enable monitoring of the PostgreSQL cluster. You also store references to the created monitoring infrastructure to use as input during the AKS cluster creation process later in the guide. This section might take some time to complete.

Note

Azure Managed Grafana instances and AKS clusters are billed independently. For more pricing information, see [Azure Managed Grafana pricing](https://azure.microsoft.com/pricing/details/managed-grafana/).

Create an Azure Managed Grafana instance using the

command.`az grafana create`

`export GRAFANA_PRIMARY="grafana-${LOCAL_NAME}-${SUFFIX}" export GRAFANA_RESOURCE_ID=$(az grafana create \ --resource-group $RESOURCE_GROUP_NAME \ --name $GRAFANA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --zone-redundancy Enabled \ --tags $TAGS \ --query "id" \ --output tsv) echo $GRAFANA_RESOURCE_ID`

Create an Azure Monitor workspace using the

command.`az monitor account create`

`export AMW_PRIMARY="amw-${LOCAL_NAME}-${SUFFIX}" export AMW_RESOURCE_ID=$(az monitor account create \ --name $AMW_PRIMARY \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --tags $TAGS \ --query "id" \ --output tsv) echo $AMW_RESOURCE_ID`

Create an Azure Monitor Log Analytics workspace using the

command.`az monitor log-analytics workspace create`

`export ALA_PRIMARY="ala-${LOCAL_NAME}-${SUFFIX}" export ALA_RESOURCE_ID=$(az monitor log-analytics workspace create \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-name $ALA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --query "id" \ --output tsv) echo $ALA_RESOURCE_ID`


## Create the AKS cluster to host the PostgreSQL cluster

In this section, you create a multizone AKS cluster with a system node pool. The AKS cluster hosts the PostgreSQL cluster primary replica and two standby replicas, each aligned to a different availability zone to enable zonal redundancy.

You also add a user node pool to the AKS cluster to host the PostgreSQL cluster. Using a separate node pool allows for control over the Azure VM SKUs used for PostgreSQL and enables the AKS system pool to optimize performance and costs. You apply a label to the user node pool that you can reference for node selection when deploying the CNPG operator later in this guide. This section might take some time to complete.

Important

If you opt to use local NVMe as your PostgreSQL storage in the later parts of this guide, you need to choose a VM SKU that supports local NVMe drives, for example, [Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized) or [GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). Update `$USER_NODE_POOL_VMSKU`

accordingly.

Create an AKS cluster using the

command.`az aks create`

`export SYSTEM_NODE_POOL_VMSKU="standard_d2s_v3" export USER_NODE_POOL_NAME="postgres" export USER_NODE_POOL_VMSKU="standard_d4s_v3" az aks create \ --name $AKS_PRIMARY_CLUSTER_NAME \ --tags $TAGS \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --generate-ssh-keys \ --node-resource-group $AKS_PRIMARY_MANAGED_RG_NAME \ --enable-managed-identity \ --assign-identity $AKS_UAMI_WORKLOAD_RESOURCEID \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --nodepool-name systempool \ --enable-oidc-issuer \ --enable-workload-identity \ --enable-cluster-autoscaler \ --min-count 2 \ --max-count 3 \ --node-vm-size $SYSTEM_NODE_POOL_VMSKU \ --enable-azure-monitor-metrics \ --azure-monitor-workspace-resource-id $AMW_RESOURCE_ID \ --grafana-resource-id $GRAFANA_RESOURCE_ID \ --api-server-authorized-ip-ranges $MY_PUBLIC_CLIENT_IP \ --tier standard \ --kubernetes-version $AKS_CLUSTER_VERSION \ --zones 1 2 3 \ --output table`

Wait for the initial cluster operation to complete using the

command so additional updates, such as adding the user node pool, don’t collide with an in-progress managed-cluster update:`az aks wait`

`az aks wait \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --created`

Add a user node pool to the AKS cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $AKS_PRIMARY_CLUSTER_NAME \ --name $USER_NODE_POOL_NAME \ --enable-cluster-autoscaler \ --min-count 3 \ --max-count 6 \ --node-vm-size $USER_NODE_POOL_VMSKU \ --zones 1 2 3 \ --labels workload=postgres \ --output table`


## Connect to the AKS cluster and create namespaces

In this section, you get the AKS cluster credentials, which serve as the keys that allow you to authenticate and interact with the cluster. Once connected, you create two namespaces: one for the CNPG controller manager services and one for the PostgreSQL cluster and its related services.

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --output none`

Create the namespace for the CNPG controller manager services, the PostgreSQL cluster, and its related services by using the

command.`kubectl create namespace`

`kubectl create namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME kubectl create namespace $PG_SYSTEM_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


You can now define another environment variable based on your desired storage option, which you reference later in the guide when deploying PostgreSQL.

You can reference the default preinstalled Premium SSD Azure Disks CSI driver storage class:

```
export POSTGRES_STORAGE_CLASS="managed-csi-premium"
```


## Update the monitoring infrastructure

The Azure Monitor workspace for Managed Prometheus and Azure Managed Grafana are automatically linked to the AKS cluster for metrics and visualization during the cluster creation process. In this section, you enable log collection with AKS Container insights and validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs.

Enable Container insights monitoring on the AKS cluster using the

command.`az aks enable-addons`

`az aks enable-addons \ --addon monitoring \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-resource-id $ALA_RESOURCE_ID \ --output table`

Validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs from the AKS cluster by inspecting the DaemonSet using the

command and the`kubectl get`

command.`az aks show`

`kubectl get ds ama-metrics-node \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system kubectl get ds ama-logs \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system az aks show \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --query addonProfiles`

Your output should resemble the following example output, with

*six*nodes total (three for the system node pool and three for the PostgreSQL node pool) and the Container insights showing`"enabled": true`

:`NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-metrics-node 6 6 6 6 6 <none> NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-logs 6 6 6 6 6 <none> { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/rg-cnpg-9vbin3p8/providers/Microsoft.OperationalInsights/workspaces/ala-cnpg-9vbin3p8", "useAADAuth": "true" }, "enabled": true, "identity": null } }`


## Create a public static IP for PostgreSQL cluster ingress

To validate deployment of the PostgreSQL cluster and use client PostgreSQL tooling, such as *psql* and *PgAdmin*, you need to expose the primary and read-only replicas to ingress. In this section, you create an Azure public IP resource that you later supply to an Azure load balancer to expose PostgreSQL endpoints for query.

Get the name of the AKS cluster node resource group using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME=$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query nodeResourceGroup \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME`

Create the public IP address using the

command.`az network public-ip create`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_NAME="$AKS_PRIMARY_CLUSTER_NAME-pip" az network public-ip create \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard \ --zone 1 2 3 \ --allocation-method static \ --output table`

Get the newly created public IP address using the

command.`az network public-ip show`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS=$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query ipAddress \ --output tsv) echo $AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS`

Get the resource ID of the node resource group using the

command.`az group show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE=$(az group show --name \ $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --query id \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE`

Assign the "Network Contributor" role to the UAMI object ID using the node resource group scope using the

command.`az role assignment create`

`az role assignment create \ --assignee-object-id ${AKS_UAMI_WORKLOAD_OBJECTID} \ --assignee-principal-type ServicePrincipal \ --role "Network Contributor" \ --scope ${AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE}`


## Install the CNPG operator in the AKS cluster

In this section, you install the CNPG operator in the AKS cluster using Helm or a YAML manifest.

Add the CNPG Helm repo using the

command.`helm repo add`

`helm repo add cnpg https://cloudnative-pg.github.io/charts`

Upgrade the CNPG Helm repo and install it on the AKS cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install cnpg \ --namespace $PG_SYSTEM_NAMESPACE \ --create-namespace \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME \ cnpg/cloudnative-pg`

Verify the operator installation on the AKS cluster using the

command.`kubectl get`

`kubectl get deployment \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_SYSTEM_NAMESPACE cnpg-cloudnative-pg`


## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-azure-rbac -->

# Use Azure role-based access control for Kubernetes Authorization

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers how to use Azure RBAC for Kubernetes Authorization, which allows for the unified management and access control across Azure resources, AKS, and Kubernetes resources. For more information, see [Azure RBAC for Kubernetes Authorization](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization).

Note

When using [integrated authentication between Microsoft Entra ID and AKS](managed-azure-ad), you can use Microsoft Entra users, groups, or service principals as subjects in [Kubernetes role-based access control (Kubernetes RBAC)](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization). With this feature, you don't need to separately manage user identities and credentials for Kubernetes. However, you still need to set up and manage Azure RBAC and Kubernetes RBAC separately.

## Before you begin

- You need the Azure CLI version 2.24.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

, with a minimum version of[1.18.3](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1183). - You need managed Microsoft Entra integration enabled on your cluster before you can add Azure RBAC for Kubernetes authorization. If you need to enable managed Microsoft Entra integration, see
[Use Microsoft Entra ID in AKS](managed-azure-ad). - If you have CRDs and are making custom role definitions, the only way to cover CRDs today is to use
`Microsoft.ContainerService/managedClusters/*/read`

. For the remaining objects, you can use the specific API groups, such as`Microsoft.ContainerService/apps/deployments/read`

. - New role assignments can take
*up to five minutes*to propagate and be updated by the authorization server. - Azure RBAC for Kubernetes Authorization requires that the Microsoft Entra tenant configured for authentication is same as the tenant for the subscription that holds your AKS cluster.

## Create a new AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization

Create an Azure resource group using the

command.`az group create`

`export RESOURCE_GROUP=<resource-group-name> export LOCATION=<azure-region> az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization using the

command.`az aks create`

`export CLUSTER_NAME=<cluster-name> az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-aad \ --enable-azure-rbac \ --generate-ssh-keys`

Your output should look similar to the following example output:

`"AADProfile": { "adminGroupObjectIds": null, "clientAppId": null, "enableAzureRbac": true, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "****-****-****-****-****" }`


## Enable Azure RBAC on an existing AKS cluster

Enable Azure RBAC for Kubernetes Authorization on an existing AKS cluster using the

command with the`az aks update`

`--enable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac`


## Disable Azure RBAC for Kubernetes Authorization from an AKS cluster

Remove Azure RBAC for Kubernetes Authorization from an existing AKS cluster using the

command with the`az aks update`

`--disable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --disable-azure-rbac`


## AKS built-in roles

AKS provides the following built-in roles:

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. It doesn't allow viewing roles or role bindings. This role doesn't allow viewing `Secrets` , since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. This role doesn't allow viewing or modifying roles or role bindings. However, this role allows accessing `Secrets` and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. This role doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. It gives full control over every resource in the cluster and in all namespaces. |

## Create role assignments for cluster access

Get your AKS resource ID using the

command.`az aks show`

`AKS_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query id --output tsv)`

Create a role assignment using the

command.`az role assignment create`

`<AAD-ENTITY-ID>`

can be a username or the client ID of a service principal. The following example creates a role assignment for the*Azure Kubernetes Service RBAC Admin*role.`az role assignment create --role "Azure Kubernetes Service RBAC Admin" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`

Note

You can create the

*Azure Kubernetes Service RBAC Reader*and*Azure Kubernetes Service RBAC Writer*role assignments scoped to a specific namespace within the cluster using thecommand and setting the scope to the desired namespace.`az role assignment create`

`az role assignment create --role "Azure Kubernetes Service RBAC Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID/namespaces/<namespace-name>`


## Create custom roles definitions

The following example custom role definition allows a user to only read deployments and nothing else. For the full list of possible actions, see [Microsoft.ContainerService operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftcontainerservice).

To create your own custom role definitions, copy the following file, replacing

`<YOUR SUBSCRIPTION ID>`

with your own subscription ID, and then save it as`deploy-view.json`

.`{ "Name": "AKS Deployment Reader", "Description": "Lets you view all deployments in cluster/namespace.", "Actions": [], "NotActions": [], "DataActions": [ "Microsoft.ContainerService/managedClusters/apps/deployments/read" ], "NotDataActions": [], "assignableScopes": [ "/subscriptions/<YOUR SUBSCRIPTION ID>" ] }`

Create the role definition using the

command, setting the`az role definition create`

`--role-definition`

to the`deploy-view.json`

file you created in the previous step.`az role definition create --role-definition @deploy-view.json`

Assign the role definition to a user or other identity using the

command.`az role assignment create`

`az role assignment create --role "AKS Deployment Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`


## Use Azure RBAC for Kubernetes Authorization with `kubectl`


Make sure you have the

[Azure Kubernetes Service Cluster User](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-user-role)built-in role, and then get the kubeconfig of your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Use Azure RBAC for Kubernetes Authorization with `kubelogin`


AKS created the [ kubelogin](https://github.com/Azure/kubelogin) plugin to help unblock scenarios such as non-interactive logins, older

`kubectl`

versions, or leveraging SSO across multiple clusters without the need to sign in to a new cluster.Use the

`kubelogin`

plugin by running the following command:`export KUBECONFIG=/path/to/kubeconfig kubelogin convert-kubeconfig`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Clean up resources

### Delete role assignment

List role assignments using the

command.`az role assignment list`

`az role assignment list --scope $AKS_ID --query [].id --output tsv`

Delete role assignments using the

command.`az role assignment delete`

`az role assignment delete --ids <LIST OF ASSIGNMENT IDS>`


### Delete role definition

Delete the custom role definition using the

command.`az role definition delete`

`az role definition delete --name "AKS Deployment Reader"`


### Delete resource group and AKS cluster

Delete the resource group and AKS cluster using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP --yes --no-wait`


## Next steps

To learn more about AKS authentication, authorization, Kubernetes RBAC, and Azure RBAC, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-cvm -->

# Use Confidential Virtual Machines (CVM) in Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Confidential Virtual Machines (CVM)](/en-us/azure/confidential-computing/confidential-vm-overview) offer strong security and confidentiality for tenants. CVMs offer VM based Hardware Trusted Execution Environment (TEE) that leverage SEV-SNP security features to deny the hypervisor and other host management code access to VM memory and state, providing defense in depth protections against operator access. These features enable node pools with CVM to target the migration of highly sensitive container workloads to AKS without any code refactoring while benefiting from the features of AKS. For example, you may require CVM if you have the following:

- Workloads that handle security critical data and/or sensitive customer data
- Services that are required to meet various compliance requirements, especially for government contracts. Without a scalable solution for securing data, this could potentially lead to the loss of accreditations and contracts.

In this article, you learn how to create AKS node pools using Confidential VM sizes.

## AKS supported confidential VM sizes

Azure offers a choice of [Trusted Execution Environment (TEE)](/en-us/azure/confidential-computing/trusted-execution-environment) options from both AMD and Intel. These TEEs allow you to create Confidential VM environments with excellent price-to-performance ratios, all without requiring any code changes.

- AMD-based Confidential VMs, use AMD SEV-SNP technology, which is introduced with third Gen AMD EPYC™ processors.
- Intel-based Confidential VMs use Intel TDX, with fourth Gen Intel® Xeon® processors.

Both technologies have different implementations. However both provide similar protections from the cloud infrastructure stack. For more information, see [CVM VM sizes](/en-us/azure/confidential-computing/virtual-machine-options).

## Security Features

CVMs offer the following security enhancements as compared to other virtual machine (VM) sizes:

- Robust hardware-based isolation between virtual machines, hypervisor, and host management code.
- Customizable attestation policies to ensure the host's compliance before deployment.
- Cloud-based Confidential OS disk encryption before the first boot.
- VM encryption keys that the platform or the customer (optionally) owns and manages.
- Secure key release with cryptographic binding between the platform's successful attestation and the VM's encryption keys.
- Dedicated virtual Trusted Platform Module (TPM) instance for attestation and protection of keys and secrets in the virtual machine.
- Secure boot capability similar to Trusted launch for Azure VMs

## How does it work?

If you're running a workload that requires enhanced confidentiality and integrity, you can benefit from memory encryption and enhanced security without code changes in your application. All pods on your CVM node are part of the same trust boundary. The nodes in a node pool created with CVM use a customized [node image](node-images) specially configured for CVM.

### Supported OS Versions

You can create CVM node pools on Linux OS types (Ubuntu and Azure Linux). However, not all OS versions support CVM node pools.

This table includes the supported OS versions:

| OS Type | OS SKU | CVM support | CVM default |
|---|---|---|---|
| Linux | `Ubuntu` |
Supported | Ubuntu 20.04 is default for K8s version 1.24-1.33. Ubuntu 24.04 is the default for K8s version 1.34-1.38. |
| Linux | `Ubuntu2204` |
Not Supported | AKS doesn't support CVM for Ubuntu 22.04. |
| Linux | `Ubuntu2404` |
Supported | CVM is supported on `Ubuntu2404` in K8s 1.32-1.38. |
| Linux | `AzureLinux` |
Supported on Azure Linux 3.0 | Azure Linux 3 is default when enabling CVM for K8s version 1.28-1.36. |
| Linux | `flatcar` |
Not supported |
|

`AzureLinuxOSGuard`

[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)doesn't support CVM.When using `Ubuntu`

or `AzureLinux`

as the `osSKU`

, if the default OS version doesn't support CVM, AKS defaults to the most recent CVM-supported version of the OS. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support CVM, AKS defaults to Ubuntu 20.04 for Linux CVM-enabled node pools.

### Limitations

The following limitations apply when adding a node pool with CVM to AKS:

- You can't use FIPS, ARM64, Trusted Launch, or Pod Sandboxing.
- You can't update an existing node pool to migrate to a CVM size. To migrate, you'll need to
[resize your node pool](resize-node-pool). - You can't use CVM with Windows node pools.
- CVM with Azure Linux is currently in preview.

## Prerequisites

Before you begin, make sure you have the following:

- An existing AKS cluster.
- CVM sizes must be available for your subscription in the region where the cluster is created. You must have sufficient quota to create a node pool with a CVM size.
- If you're using Azure Linux os, you need to install the
`aks-preview`

extension, update the`aks-preview`

extension, and register the preview feature flag. If you're using Ubuntu, you can skip these steps.

### If you are using Azure Linux

CVMs for Ubuntu is GA, but CVMs with Azure Linux is currently still in preview. If you would like to use CVM node pools with Azure Linux as the OS of choice, ensure you enable the extension and register the flag.

#### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


#### Register `AzureLinuxCVMPreview`

feature flag

Register the

`AzureLinuxCVMPreview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AzureLinuxCVMPreview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AzureLinuxCVMPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a node pool with a CVM to your AKS cluster

Add a node pool with a CVM to your AKS cluster using the

command and set the`az aks nodepool add`

`node-vm-size`

to a supported[VM size](/en-us/azure/confidential-computing/virtual-machine-options).`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --node-count 3 \ --node-vm-size Standard_DC4as_v5`


If you don't specify the `osSKU`

or `osType`

, AKS defaults to `--os-type Linux`

and `--os-sku Ubuntu`

.

## Upgrade an existing node pool with a CVM to Ubuntu 24.04

Upgrade an existing node pool with a CVM to Ubuntu 24.04 from Ubuntu 20.04 using the

command. Set the`az aks nodepool update`

`os-sku`

as`Ubuntu2404`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --os-sku Ubuntu2404`


Note

A node pool which is Ubuntu 24.04 with a CVM is supported from AKS cluster 1.33 version. Additionally, before Ubuntu 24.04 becomes GA, you need to register the `Ubuntu2404Preview`

feature. For more information, see [ here](/en-us/azure/aks/upgrade-os-version#register-ubuntu2404preview-feature-flag) to register the feature.

## Verify the node pool uses CVM

Verify a node pool uses CVM using the

command and verify the`az aks nodepool show`

`vmSize`

is`Standard_DCa4_v5`

.`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize'`

The following example command and output shows the node pool uses CVM:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize' "Standard_DC4as_v5"`

Verify a node pool uses a CVM image using the

command.`az aks nodepool list`

`az aks nodepool list \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion'`

The following example command and output shows the node pool uses an Ubuntu 20.04 CVM image:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion' "AKSUbuntu-2004cvmcontainerd-202507.02.0"`


## Remove a node pool with CVM from an AKS cluster

Remove a node pool with CVM from an AKS cluster using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool`


## Next steps

In this article, you learned how to add a node pool with CVM to an AKS cluster.

- For more information about CVM, see
[Confidential VM node pools support on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks). - To migrate an existing node pool to a CVM vm size, you can
[resize your node pool](resize-node-pool). - If you're only interested in enabling Trusted Launch on your node pools, see
[Trusted Launch on AKS](use-trusted-launch).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/http-proxy -->

# HTTP proxy support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to configure Azure Kubernetes Service (AKS) clusters to use an HTTP proxy for outbound internet access.

AKS clusters deployed into managed or custom virtual networks have certain outbound dependencies that are necessary to function properly, which created problems in environments requiring internet access to be routed through HTTP proxies. Nodes had no way of bootstrapping the configuration, environment variables, and certificates necessary to access internet services.

The HTTP proxy feature adds HTTP proxy support to AKS clusters, exposing a straightforward interface that you can use to secure AKS-required network traffic in proxy-dependent environments. With this feature, both AKS nodes and pods are configured to use the HTTP proxy. The feature also enables installation of a trusted certificate authority onto the nodes as part of bootstrapping a cluster. More complex solutions might require creating a chain of trust to establish secure communications across the network.

## Limitations and considerations

The following scenarios are **not** supported:

- Different proxy configurations per node pool
- User/Password authentication
- Custom certificate authorities (CAs) for API server communication
- AKS clusters with Windows node pools
- Node pools using Virtual Machine Availability Sets (VMAS)
- Using * as wildcard attached to a domain suffix for noProxy

`httpProxy`

, `httpsProxy`

, and `trustedCa`

have no value by default. Pods are injected with the following environment variables:

`HTTP_PROXY`

`http_proxy`

`HTTPS_PROXY`

`https_proxy`

`NO_PROXY`

`no_proxy`


To disable the injection of the proxy environment variables, you need to annotate the Pod with `"kubernetes.azure.com/no-http-proxy-vars":"true"`

.

## Before you begin

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a configuration file with HTTP proxy values

Create a file and provide values for `httpProxy`

, `httpsProxy`

, and `noProxy`

. If your environment requires it, provide a value for `trustedCa`

.

The schema for the config file looks like this:

```
{
"httpProxy": "string",
"httpsProxy": "string",
"noProxy": [
"string"
],
"trustedCa": "string"
}
```


Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate **must** support `Subject Alternative Names(SANs)`

instead of the deprecated Common Name certs.

There are differences in applications on how to comply with the environment variable `http_proxy`

, `https_proxy`

, and `no_proxy`

. Curl and Python don't support CIDR in `no_proxy`

, but Ruby does.

Example input:

```
{
"httpProxy": "http://myproxy.server.com:8080",
"httpsProxy": "https://myproxy.server.com:8080",
"noProxy": [
"localhost",
"127.0.0.1"
],
"trustedCA": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUgvVENDQmVXZ0F3SUJB...S0tLS0="
}
```


## Create a cluster with an HTTP proxy configuration using the Azure CLI

You can configure an AKS cluster with an HTTP proxy configuration during cluster creation.

Use the

command and pass in your configuration as a JSON file.`az aks create`

`az aks create \ --name $clusterName \ --resource-group $resourceGroup \ --http-proxy-config aks-proxy-config.json \ --generate-ssh-keys`

Your cluster should initialize with the HTTP proxy configured on the nodes.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update a cluster to update or enable HTTP proxy

Enable or update HTTP proxy configurations on an existing cluster using the

command.`az aks update`

For example, let's say you created a new file with the base64 encoded string of the new CA cert called

*aks-proxy-config-2.json*. You can update the proxy configuration on your cluster with the following command:`az aks update --name $clusterName --resource-group $resourceGroup --http-proxy-config aks-proxy-config-2.json`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster (Preview)

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy (preview)

Update your cluster to disable HTTP proxy using the

command with`az aks update`

`--disable-http-proxy`

flag.`az aks update --name $clusterName --resource-group $resourceGroup --disable-http-proxy`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating the HTTP proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, the proxy configuration is saved in the database but the proxy variables are removed from the pods and nodes.

To re-enable HTTP proxy on an existing cluster, use the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-http-proxy`

flag.```
az aks update --name $clusterName --resource-group $resourceGroup --enable-http-proxy
```


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Important

If you had an HTTP proxy configuration on your cluster before disabling, the existing HTTP proxy configuration automatically applies when you re-enable HTTP proxy on that cluster. We recommend verifying the configuration to ensure it meets your current requirements before proceeding. If you want to change your HTTP proxy configuration after re-enabling HTTP proxy, follow the steps to [Update the HTTP proxy configuration on an existing cluster](#update-a-cluster-to-update-or-enable-http-proxy).

## Configure an HTTP proxy configuration using an Azure Resource Manager (ARM) template

You can deploy an AKS cluster with an HTTP proxy using an ARM template.

Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate

**must**support`Subject Alternative Names (SANs)`

instead of the deprecated Common Name certs.There are differences in applications on how to comply with the environment variable

`http_proxy`

,`https_proxy`

, and`no_proxy`

. Curl and Python don't support CIDR in`no_proxy`

, but Ruby does.Create a template with HTTP proxy parameters. In your template, provide values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the HTTP Proxy configuration. Your cluster should initialize with your HTTP proxy configured on the nodes.


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update an ARM template to configure HTTP proxy

In your template, provide new values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

.The same schema used for CLI deployment exists in the

`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the updated HTTP Proxy configuration.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster using an ARM template (Preview)

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy

Update your cluster ARM template to disable HTTP proxy by setting

`enabled`

to`false`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "false", } }`

Deploy your ARM template with HTTP Proxy disabled.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating that the HTTP Proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, you can no longer add HTTP proxy configurations to that cluster.

If you want to re-enable HTTP proxy, follow the steps to [Update an HTTP proxy configuration using an ARM template](#update-an-arm-template-to-configure-http-proxy).

## Istio add-on HTTP proxy for External Services

If you're using the [Istio-based service mesh add-on for AKS](istio-about), you must create a Service Entry to enable your applications in the mesh to access noncluster or external resources via the HTTP proxy.

For example:

```
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: proxy
spec:
hosts:
- my-company-proxy.com # ignored
addresses:
- $PROXY_IP/32
ports:
- number: $PROXY_PORT
name: tcp
protocol: TCP
location: MESH_EXTERNAL
```


Create a file and provide values for

`PROXY_IP`

and`PROXY_PORT`

.You can deploy the Service Entry using:

`kubectl apply -f service_proxy.yaml`


## Monitoring add-on configuration

HTTP proxy with the monitoring add-on supports the following configurations:

- Outbound proxy without authentication
- Outbound proxy with trusted cert for Log Analytics endpoint

The following configuration isn't supported:

- Custom Metrics and Recommended Alerts features when using a proxy with trusted certificates

## Next steps

For more information regarding the network requirements of AKS clusters, see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-authentication-microsoft-entra-id -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster -->

# Automatically upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Part of the AKS cluster lifecycle involves performing periodic upgrades to the latest Kubernetes version. It's important you apply the latest security releases or upgrade to get the latest features. Before you learn about automatic upgrades, make sure you understand the [AKS cluster upgrade fundamentals](upgrade-cluster).

Note

Any upgrade operation, whether performed manually or automatically, upgrades the node image version if it's not already on the latest version. The latest version is contingent on a full AKS release and can be determined by visiting the [AKS release tracker](release-tracker).

Autoupgrade first upgrades the control plane, and then upgrades agent pools one by one.

## Why use cluster autoupgrade

Cluster autoupgrade provides a *set once and forget* mechanism that yields tangible time and operational cost benefits. You don't need to stop your workloads, redeploy your workloads, or create a new AKS cluster. By enabling autoupgrade, you can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes.

AKS follows a strict supportability versioning window. With properly selected autoupgrade channels, you can avoid clusters falling into an unsupported version. For more on the AKS support window, see [Alias minor versions](supported-kubernetes-versions).

## Customer versus AKS-initiated autoupgrades

You can specify cluster autoupgrade specifics using the following guidance. The upgrades occur based on your specified cadence and are recommended to remain on supported Kubernetes versions.

AKS also initiates autoupgrades for unsupported clusters. When a cluster in an n-3 version (where n is the latest supported AKS GA minor version) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support [policy](supported-kubernetes-versions). Automatically upgrading a platform supported cluster to a supported version is enabled by default. Stopped node pools are upgraded during an autoupgrade operation. The upgrade applies to nodes when the node pool is started. To minimize disruptions, set up [maintenance windows](planned-maintenance).

## Cluster autoupgrade limitations

If you're using cluster autoupgrade, you can no longer upgrade the control plane first, and then upgrade the individual node pools. Cluster autoupgrade always upgrades the control plane and the node pools together. You can't upgrade the control plane only. Running the `az aks upgrade --control-plane-only`

command raises the following error:

```
NotAllAgentPoolOrchestratorVersionSpecifiedAndUnchanged: Using managed cluster api, all Agent pools' OrchestratorVersion must be all specified or all unspecified. If all specified, they must be stay unchanged or the same with control plane.
```


If using the `node-image`

(legacy and not to be used) cluster autoupgrade channel or the `NodeImage`

node image autoupgrade channel, Linux [unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates) are disabled by default.

## Cluster autoupgrade channels

Automatically completed upgrades are functionally the same as manual upgrades. The [selected autoupgrade channel](planned-maintenance) determines the timing of upgrades. When making changes to autoupgrade, allow 24 hours for the changes to take effect. Automatically upgrading a cluster follows the same process as manually upgrading a cluster. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

The following upgrade channels are available:

| Channel | Action | Example |
|---|---|---|
`none` |
disables autoupgrades and keeps the cluster at its current version of Kubernetes. | Default setting if left unchanged. |
`patch` |
automatically upgrades the cluster to the latest supported patch version when it becomes available while keeping the minor version the same. | For example, if a cluster runs version 1.17.7, and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.17.9. |
`stable` |
automatically upgrades the cluster to the latest supported patch release on minor version N-1, where N is the latest supported minor version. |
For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.18.6. |
`rapid` |
automatically upgrades the cluster to the latest supported patch release on the latest supported minor version. | In cases where the cluster's Kubernetes version is an N-2 minor version, where N is the latest supported minor version, the cluster first upgrades to the latest supported patch version on N-1 minor version. For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster first upgrades to 1.18.6, then upgrades to 1.19.1. |
`node-image` (legacy) |
automatically upgrades the node image to the latest version available. | Microsoft provides patches and new images for image nodes frequently (weekly), but your running nodes don't get the new images unless you do a node image upgrade. Turning on the node-image channel automatically updates your node images whenever a new version is available. If you use this channel, Linux [unattended upgrades] are disabled by default. Node image upgrades work on patch versions that are deprecated, so long as the minor Kubernetes version is still supported. This channel is no longer recommended and is planned for deprecation in future. For an option that can automatically upgrade node images, see the `NodeImage` channel in
|

Note

Keep the following information in mind when using cluster autoupgrade:

Cluster autoupgrade only updates to GA versions of Kubernetes and doesn't update to preview versions.

With AKS, you can create a cluster without specifying the exact patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. To learn more, see

[AKS support window](supported-kubernetes-versions).Autoupgrade requires the cluster's Kubernetes version to be within the

[AKS support window](supported-kubernetes-versions), even if using the`node-image`

channel.If you're using the preview API

`11-02-preview`

or later, and you select the`node-image`

cluster autoupgrade channel, the[node image autoupgrade channel](auto-upgrade-node-image)automatically sets to`NodeImage`

.Each cluster can only be associated with a single autoupgrade channel. The reason is because your specified channel determines the Kubernetes version that runs on the cluster.

If your cluster has no autoupgrade channel and you enable it for Long-Term Support (LTS), the cluster defaults to a

`patch`

autoupgrade channel.

## Use cluster autoupgrade with a new AKS cluster

Set the autoupgrade channel when creating a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and the

`auto-upgrade-channel`

parameter.```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster"
az aks create --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable --generate-ssh-keys
```


## Use cluster autoupgrade with an existing AKS cluster

Set the autoupgrade channel on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`auto-upgrade-channel`

parameter.```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable
```


Results:

```
{
"id": "/subscriptions/aaaa6a6a-bb7b-cc8c-dd9d-eeeeee0e0e0e/resourceGroups/myResourceGroupabc123/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
"properties": {
"autoUpgradeChannel": "stable",
"provisioningState": "Succeeded"
}
}
```


## Use autoupgrade with Planned Maintenance

If using Planned Maintenance and cluster autoupgrade, your upgrade starts during your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of *four hours or more*.

For more information on how to set a maintenance window with Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Best practices for cluster autoupgrade

Use the following best practices to help maximize your success when using autoupgrade:

- To ensure your cluster is always in a supported version, for example within the N-2 rule, choose either
`stable`

or`rapid`

channels. - If you're interested in getting the latest patches as soon as possible, use the
`patch`

channel. The`node-image`

channel is a good fit if you want your agent pools to always run the most recent node images. - To automatically upgrade node images while using a different cluster upgrade channel, consider using the
[node image autoupgrade](auto-upgrade-node-image)`NodeImage`

channel. - Follow
[Operator best practices](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets). - Follow
[PodDisruptionBudget (PDB) best practices](https://kubernetes.io/docs/tasks/run-application/configure-pdb/). - For upgrade troubleshooting information, see the
[AKS troubleshooting documentation](/en-us/support/azure/azure-kubernetes/welcome-azure-kubernetes).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-tool-calling -->

# Integrate tool calling with LLM Inference with the AI toolchain operator add-on on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS) with support for OpenAI-style tool calling. You also learn how to validate tool calling functionality using vLLM metrics and local function mocks.

## What is tool calling?

Tool calling enables large language models (LLMs) to interface with external functions, APIs, or services. Instead of just generating text, an LLM can decide:

- "I need to call a weather API."
- "I need to use a calculator."
- "I should search a database."

It does this by invoking a defined “tool” with parameters it chooses based on the user’s request. Tool calling is useful for:

- Chatbots that book, summarize, or calculate.
- Enterprise LLM applications where hallucination must be minimized.
- Agent frameworks (AutoGen, LangGraph, LangChain, AgentOps, etc.).

In production environments, AI-enabled applications often demand more than natural language generation; they require the ability to take action based on user intent. Tool calling empowers LLMs to extend beyond text responses by invoking external tools, APIs, or custom logic in real time. This bridges the gap between language understanding and execution, enabling developers to build interactive AI assistants, agents, and automation workflows that are both accurate and useful. Instead of relying on static responses, LLMs can now access live data, trigger services, and complete tasks on behalf of users, both safely and reliably.

When deployed on AKS, tool calling becomes scalable, secure, and production ready. Kubernetes provides the flexibility to orchestrate inference workloads using high-performance runtimes like vLLM, while ensuring observability and governance of tool usage. With this pattern, AKS operators and app developers can more seamlessly update models or tools independently and deploy advanced AI features without compromising reliability.

As a result, tool calling on AKS is now a foundational pattern for building modern AI apps that are context-aware, action-capable, and enterprise-ready.

### Tool calling with KAITO

To streamline this deployment model, the AI toolchain operator (KAITO) add-on for AKS provides a managed solution for running inference services with [tool calling support](https://kaito-project.github.io/kaito/docs/tool-calling/). By leveraging KAITO inference workspaces, you can quickly spin up scalable, GPU-accelerated model endpoints with built-in support for tool calling and OpenAI-compatible APIs. This eliminates the operational overhead of configuring runtimes, managing dependencies, or scaling infrastructure manually.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster. - A deployed KAITO inference workspace that supports tool calling. Refer to the official
[KAITO tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/)documentation for the tool calling supported models with vLLM. - You deployed the
`workspace‑phi‑4-mini-toolcall`

[KAITO workspace](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_tool_calling.yaml)with the default configuration.

## Confirm the KAITO inference workspace is running

Monitor your workspace deployment with the

`kubectl get`

command.`kubectl get workspace workspace‑phi‑4‑mini-toolcall -w`

In the output, you want to verify the resource (

`ResourceReady`

) and inference (`InferenceReady`

) are ready and the workspace succeeded (`WorkspaceSucceeded`

being`true`

).

## Confirm the inference API is ready to serve

Once the

[workspace is ready](#confirm-the-kaito-inference-workspace-is-running), find the service endpoint using the`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check the

`/v1/models`

endpoint to confirm the LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

To ensure the LLM is deployed, and the API is working, your output should be similar to the following:

`... { "object": "list", "data": [ { "id": "phi‑4‑mini‑instruct", ... ... } ] } ...`


## Test the named function tool‐calling

In this example, the `workspace‑phi‑4‑mini-toolcall`

workspace supports named function tool-calling by default, so we can confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure.

The Python snippet we use in this section is from the [KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/#examples) and uses an OpenAI‑compatible client.

Confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure. This example:

- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at
`http://localhost:8000/v1`

and accepts OpenAI-style API calls. - Simulates the backend logic for a tool called
`get_weather`

. (In a real scenario, this would call a weather API.) - Describes the tool interface; the
`Phi-4-mini`

LLM will see this tool and decide whether to use it based on the user's input. - Sends a sample chat message to the model and provides the tool spec. The setting
`tool_choice="auto"`

allows the LLM to decide if it should call a tool based on the prompt. - In this case, the user's request was relevant to the
`get_weather`

tool, so we simulate the execution of the tool, calling the local function with the model's chosen arguments.

`from openai import OpenAI import json # local server client = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy") def get_weather(location: str, unit: str) -> str: return f"Getting the weather for {location} in {unit}..." tool_functions = {"get_weather": get_weather} tools = [{ "type": "function", "function": { "name": "get_weather", "description": "Get the current weather in a given location", "parameters": { "type": "object", "properties": { "location": {"type": "string"}, "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]} }, "required": ["location", "unit"] } } }] response = client.chat.completions.create( model="phi‑4‑mini‑instruct", # or client.models.list().data[0].id messages=[{"role": "user", "content": "What's the weather like in San Francisco?"}], tools=tools, tool_choice="auto" ) # Inspect response tool_call = response.choices[0].message.tool_calls[0].function args = json.loads(tool_call.arguments) print("Function called:", tool_call.name) print("Arguments:", args) print("Result:", tool_functions[tool_call.name](**args))`

Your output should look similar to the following:

`Function called: get_weather Arguments: {"location": "San Francisco, CA", "unit": "fahrenheit"} Result: Getting the weather for San Francisco, CA in fahrenheit...`

The “tool_calls” field comes back, meaning the

`Phi-4-mini`

LLM decided to invoke the function. Now, a sample tool call has been successfully parsed and executed based on the model’s decision to confirm end-to-end tool calling behavior with the KAITO inference deployment.- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at

## Troubleshooting

### Model preset doesn’t support tool calling

If you pick a model that isn't on the supported list, tool calling might not work. Make sure you [review the KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/), which explicitly lists which presets support tool calling.

### Misaligned runtime

The KAITO inference must use [vLLM runtime for tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/#supported-inference-runtimes) (HuggingFace Transformers runtime generally doesn’t support tool calling in KAITO).

### Network / endpoint issues

If port-forwarding, ensure the service ports are correctly forwarded. If the external MCP server is unreachable, will error out.

### Timeouts

External MCP server calls might take time. Make sure the adapter or client timeout is sufficiently high.

### Authentication

If the external MCP server requires authentication (API key, header, etc.), ensure you supply correct credentials.

## Next steps

- Set up
[vLLM monitoring in the AI toolchain operator add-on](ai-toolchain-operator-monitoring)with Prometheus and Grafana on AKS. - Learn about
[MCP server support with KAITO](ai-toolchain-operator-mcp)and test standardized tool calling examples on your AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-telemetry -->

# Telemetry API for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Istio can [generate metrics, distributed traces, and access logs](https://istio.io/latest/docs/concepts/observability/) for all workloads in the mesh. The Istio-based service mesh add-on for Azure Kubernetes Service (AKS) provides telemetry customization options through the [shared MeshConfig](istio-meshconfig) and the Istio Telemetry API `v1`

for Istio add-on minor revisions `asm-1-22`

and higher.

Note

While the [Istio MeshConfig](istio-meshconfig) also provides options for configuring telemetry globally across the mesh, the Telemetry API offers more granular control over telemetry settings on a per-service or per-workload basis. As the Istio community continues to invest in the Telemetry API, it is now the preferred method for telemetry configuration. We encourage migrating to the Telemetry API for configuring telemetry to be collected in the mesh.

## Prerequisites

- You must be on revision
`asm-1-22`

or higher. For information on how to perform minor version upgrades, see the[Istio add-on upgrade documentation](istio-upgrade).

## Configure Telemetry resources

The following example demonstrates how Envoy access logging can be enabled across the mesh for the Istio add-on via the Telemetry API using `asm-1-22`

(adjust the revision as needed). For guidance on other Telemetry API customizations for the add-on, see the [Telemetry API support scope](#telemetry-api-support-scope) section and the [Istio documentation](https://istio.io/latest/docs/reference/config/telemetry/).

### Deploy sample applications

Label the namespace for sidecar injection:

```
kubectl label ns default istio.io/rev=asm-1-22
```


Deploy the `sleep`

application and set the `SOURCE_POD`

environment variable:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/sleep/sleep.yaml
export SOURCE_POD=$(kubectl get pod -l app=sleep -o jsonpath={.items..metadata.name})
```


Then, deploy the `httpbin`

application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/httpbin/httpbin.yaml
```


### Enable Envoy access logging with the Istio Telemetry API

Deploy the following Istio `v1`

Telemetry API resource to enable Envoy access logging for the entire mesh:

```
cat <<EOF | kubectl apply -n aks-istio-system -f -
apiVersion: telemetry.istio.io/v1
kind: Telemetry
metadata:
name: mesh-logging-default
spec:
accessLogging:
- providers:
- name: envoy
EOF
```


### Test access logs

Send a request from `sleep`

to `httpbin`

:

```
kubectl exec "$SOURCE_POD" -c sleep -- curl -sS -v httpbin:8000/status/418
```


Verify that access logs are visible for the `sleep`

pod:

```
kubectl logs -l app=sleep -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.690Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 12 11 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" outbound|8000||httpbin.default.svc.cluster.local 10.244.0.12:53336 10.0.112.220:8000 10.244.0.12:42360 - default
```


Now, verify that access logs are visible for the `httpbin`

pod:

```
kubectl logs -l app=httpbin -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.696Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 2 1 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" inbound|8080|| 127.0.0.6:55401 10.244.0.13:8080 10.244.0.12:53336 outbound_.8000_._.httpbin.default.svc.cluster.local default
```


## Telemetry API support scope

For the Istio service mesh add-on for AKS, Telemetry API fields are classified as `allowed`

, `supported`

, and `blocked`

values. For more information about the Istio add-on's support policy for features and mesh configurations, see the Istio add-on [support policy document](istio-support-policy#allowed-supported-and-blocked-customizations).

The following Telemetry API configurations are either `allowed`

or `supported`

for the Istio add-on. Any field not included in this table is `blocked`

.

Telemetry API Field |
Supported/Allowed |
Notes |
|---|---|---|
`accessLogging.match` |
Supported | - |
`accessLogging.disabled` |
Supported | - |
`accessLogging.providers` |
Allowed | The default `envoy` access log provider is supported. For a managed experience for log collection and querying, see
`allowed` but unsupported. |
`metrics.overrides` |
Supported | - |
`metrics.providers` |
Allowed | Metrics collection with
`allowed` but unsupported. |

`tracing.*`

`allowed`

but unsupported.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-scenarios-hub -->

# AKS upgrade scenarios: Choose your path

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrading Azure Kubernetes Service (AKS) clusters safely requires the right strategy for your specific situation. Use this hub to quickly identify your scenario and get targeted guidance.

## What this article covers

This decision hub helps you choose the right AKS upgrade approach based on:

- A quick scenario finder with time constraints and priorities.
- Emergency upgrade paths for critical security responses.
- A strategy matrix that compares downtime tolerance and complexity.
- Role-based guidance for site reliability engineers, database administrators, developers, and security teams.
- Decision trees for complex multi-environment setups.

This hub is best for first-time upgraders, teams that need to evaluate options, and complex environments that require tailored approaches.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-aks-cluster).

## Quick scenario finder

What's your primary concern? Select your answer from the following table.

| My priority | Time constraint | Go to |
|---|---|---|
| Zero production downtime | Upgrade needed within hours |
|

[Staged fleet upgrades](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)[Safe version intake](aks-production-upgrade-strategies#scenario-3-safe-kubernetes-version-intake)[Fast security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)[Stateful workload patterns](stateful-workload-upgrades)[Seamless architecture](aks-production-upgrade-strategies#scenario-5-application-architecture-for-seamless-upgrades)## Emergency upgrade (30-90 minutes)

If you need a critical security patch now, select a link for instructions:

**Immediate action:**[Automated security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)**With stateful workloads:**[Database safety patterns](stateful-workload-upgrades#emergency-upgrade-checklist)**Rollback ready:**[Quick recovery guide](aks-production-upgrade-strategies#emergency-rollback-procedures)

## Upgrade strategy matrix

Find your ideal approach based on business constraints.

| Downtime tolerance | Environment | Best strategy | Time investment |
|---|---|---|---|
| <2 minutes | Production | Blue-green deployment | 45-60 min |
| <30 seconds | Stateful apps | Ferris wheel pattern | 60-90 min |
| Planned window | Multi-environment | Staged fleet upgrade | 2-4 hours |
| Zero tolerance | Mission-critical | Application architecture | Ongoing |

## Key upgrade topics

### Core upgrade mechanics

### Production-ready strategies

[Scenario-based production upgrades](aks-production-upgrade-strategies)[Stateful workload upgrade patterns](stateful-workload-upgrades)[Cross-environment upgrade staging](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)

### Advanced topics

## Quick wins (5-15 minutes)

Immediate actions that you can take:

**Pre-upgrade health check:**Run[cluster diagnostics](aks-diagnostics).**Backup validation:**Verify your[disaster recovery](ha-dr-overview)setup.**Monitoring setup:**Enable[upgrade notifications](aks-communication-manager).**Team preparation:**Review[support policies](support-policies).

## Learning path

If you're new to AKS upgrades, follow this learning sequence:

**Learn:**Learn about[Kubernetes concepts](core-aks-concepts)and read the[Upgrade overview](upgrade-cluster).**Practice:**Take the tutorial on how to[upgrade an AKS cluster](tutorial-kubernetes-upgrade-cluster).**Production:**Use the[production strategies](aks-production-upgrade-strategies).**Optimize:**Find out about[stateful patterns](stateful-workload-upgrades).

## Pro tips

**Always test in nonproduction first:**Perform tests even for emergency patches.**Monitor during upgrades:**Set up[real-time alerts](aks-communication-manager).**Plan for rollback:**Have a tested recovery procedure.**Communicate with teams:**Coordinate with app owners during upgrades.

## Related content

- For more help, choose your scenario from the preceding options or start with
[Production upgrade strategies](aks-production-upgrade-strategies). - For more information, see
[AKS support options](aks-support-help)or the[Troubleshooting guide](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-postgresql-ha -->

# Create infrastructure for deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create the infrastructure resources needed to deploy a highly available PostgreSQL database on AKS using the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- Review the deployment overview and make sure you meet all the prerequisites in
[How to deploy a highly available PostgreSQL database on AKS with Azure CLI](postgresql-ha-overview). [Set environment variables](#set-environment-variables)for use throughout this guide.[Install the required extensions](#install-required-extensions).

## Set environment variables

Set the following environment variables for use throughout this guide:

```
export SUFFIX=$(cat /dev/urandom | LC_ALL=C tr -dc 'a-z0-9' | fold -w 8 | head -n 1)
export LOCAL_NAME="cnpg"
export TAGS="owner=user"
export RESOURCE_GROUP_NAME="rg-${LOCAL_NAME}-${SUFFIX}"
export PRIMARY_CLUSTER_REGION="canadacentral"
export AKS_PRIMARY_CLUSTER_NAME="aks-primary-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_MANAGED_RG_NAME="rg-${LOCAL_NAME}-primary-aksmanaged-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME="pg-primary-fedcred1-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_PG_DNSPREFIX=$(echo $(echo "a$(openssl rand -hex 5 | cut -c1-11)"))
export AKS_UAMI_CLUSTER_IDENTITY_NAME="mi-aks-${LOCAL_NAME}-${SUFFIX}"
export AKS_CLUSTER_VERSION="1.32"
export PG_NAMESPACE="cnpg-database"
export PG_SYSTEM_NAMESPACE="cnpg-system"
export PG_PRIMARY_CLUSTER_NAME="pg-primary-${LOCAL_NAME}-${SUFFIX}"
export PG_PRIMARY_STORAGE_ACCOUNT_NAME="hacnpgpsa${SUFFIX}"
export PG_STORAGE_BACKUP_CONTAINER_NAME="backups"
export MY_PUBLIC_CLIENT_IP=$(dig +short myip.opendns.com @resolver3.opendns.com)
```


## Install required extensions

Install the extensions needed for Kubernetes integration and monitoring:

```
az extension add --upgrade --name k8s-extension --yes
az extension add --upgrade --name amg --yes
```


As a prerequisite for using `kubectl`

, you need to first install [Krew](https://krew.sigs.k8s.io/), followed by the installation of the [CNPG plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). These installations enable the management of the PostgreSQL operator using the subsequent commands.

```
(
set -x; cd "$(mktemp -d)" &&
OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
KREW="krew-${OS}_${ARCH}" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
tar zxvf "${KREW}.tar.gz" &&
./"${KREW}" install krew
)
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
kubectl krew install cnpg
```


## Create a resource group

Create a resource group to hold the resources you create in this guide using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create \
--name $RESOURCE_GROUP_NAME \
--location $PRIMARY_CLUSTER_REGION \
--tags $TAGS \
--query 'properties.provisioningState' \
--output tsv
```


## Create a user-assigned managed identity

In this section, you create a user-assigned managed identity (UAMI) to allow the CNPG PostgreSQL to use an AKS workload identity to access Azure Blob Storage. This configuration allows the PostgreSQL cluster on AKS to connect to Azure Blob Storage without a secret.

Create a user-assigned managed identity using the

command.`az identity create`

`AKS_UAMI_WI_IDENTITY=$(az identity create \ --name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --output json)`

Enable AKS workload identity and generate a service account to use later in this guide using the following commands:

`export AKS_UAMI_WORKLOAD_OBJECTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.principalId') export AKS_UAMI_WORKLOAD_RESOURCEID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.id') export AKS_UAMI_WORKLOAD_CLIENTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.clientId') echo "ObjectId: $AKS_UAMI_WORKLOAD_OBJECTID" echo "ResourceId: $AKS_UAMI_WORKLOAD_RESOURCEID" echo "ClientId: $AKS_UAMI_WORKLOAD_CLIENTID"`


The object ID is a unique identifier for the client ID (also known as the application ID) that uniquely identifies a security principal of type *Application* within the Microsoft Entra ID tenant. The resource ID is a unique identifier to manage and locate a resource in Azure. These values are required to enabled AKS workload identity.

The CNPG operator automatically generates a service account called *postgres* that you use later in the guide to create a federated credential that enables OAuth access from PostgreSQL to Azure Storage.

## Create a storage account in the primary region

Create an object storage account to store PostgreSQL backups in the primary region using the

command.`az storage account create`

`az storage account create \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard_ZRS \ --kind StorageV2 \ --query 'provisioningState' \ --output tsv`

Create the storage container to store the Write Ahead Logs (WAL) and regular PostgreSQL on-demand and scheduled backups using the

command.`az storage container create`

`az storage container create \ --name $PG_STORAGE_BACKUP_CONTAINER_NAME \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --auth-mode login`

Example output:

`{ "created": true }`

Note

If you encounter the error message:

`The request may be blocked by network rules of storage account. Please check network rule set using 'az storage account show -n accountname --query networkRuleSet'. If you want to change the default action to apply when no rule matches, please use 'az storage account update'`

. Make sure to verify user permissions for Azure Blob Storage and, if**necessary**, elevate your role to`Storage Blob Data Owner`

using the commands provided and after retry thecommand.`az storage container create`

`export USER_ID=$(az ad signed-in-user show --query id --output tsv) export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) az role assignment list --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID --output table az role assignment create \ --assignee-object-id $USER_ID \ --assignee-principal-type User \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --role "Storage Blob Data Owner" \ --output tsv`


## Assign RBAC to storage accounts

To enable backups, the PostgreSQL cluster needs to read and write to an object store. The PostgreSQL cluster running on AKS uses a workload identity to access the storage account via the CNPG operator configuration parameter [ inheritFromAzureAD](https://cloudnative-pg.io/documentation/1.23/appendixes/object_stores/#azure-blob-storage).

Get the primary resource ID for the storage account using the

command.`az storage account show`

`export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) echo $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID`

Assign the "Storage Blob Data Contributor" Azure built-in role to the object ID with the storage account resource ID scope for the UAMI associated with the managed identity for each AKS cluster using the

command.`az role assignment create`

`az role assignment create \ --role "Storage Blob Data Contributor" \ --assignee-object-id $AKS_UAMI_WORKLOAD_OBJECTID \ --assignee-principal-type ServicePrincipal \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --query "id" \ --output tsv`


## Set up monitoring infrastructure

In this section, you deploy an instance of Azure Managed Grafana, an Azure Monitor workspace, and an Azure Monitor Log Analytics workspace to enable monitoring of the PostgreSQL cluster. You also store references to the created monitoring infrastructure to use as input during the AKS cluster creation process later in the guide. This section might take some time to complete.

Note

Azure Managed Grafana instances and AKS clusters are billed independently. For more pricing information, see [Azure Managed Grafana pricing](https://azure.microsoft.com/pricing/details/managed-grafana/).

Create an Azure Managed Grafana instance using the

command.`az grafana create`

`export GRAFANA_PRIMARY="grafana-${LOCAL_NAME}-${SUFFIX}" export GRAFANA_RESOURCE_ID=$(az grafana create \ --resource-group $RESOURCE_GROUP_NAME \ --name $GRAFANA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --zone-redundancy Enabled \ --tags $TAGS \ --query "id" \ --output tsv) echo $GRAFANA_RESOURCE_ID`

Create an Azure Monitor workspace using the

command.`az monitor account create`

`export AMW_PRIMARY="amw-${LOCAL_NAME}-${SUFFIX}" export AMW_RESOURCE_ID=$(az monitor account create \ --name $AMW_PRIMARY \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --tags $TAGS \ --query "id" \ --output tsv) echo $AMW_RESOURCE_ID`

Create an Azure Monitor Log Analytics workspace using the

command.`az monitor log-analytics workspace create`

`export ALA_PRIMARY="ala-${LOCAL_NAME}-${SUFFIX}" export ALA_RESOURCE_ID=$(az monitor log-analytics workspace create \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-name $ALA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --query "id" \ --output tsv) echo $ALA_RESOURCE_ID`


## Create the AKS cluster to host the PostgreSQL cluster

In this section, you create a multizone AKS cluster with a system node pool. The AKS cluster hosts the PostgreSQL cluster primary replica and two standby replicas, each aligned to a different availability zone to enable zonal redundancy.

You also add a user node pool to the AKS cluster to host the PostgreSQL cluster. Using a separate node pool allows for control over the Azure VM SKUs used for PostgreSQL and enables the AKS system pool to optimize performance and costs. You apply a label to the user node pool that you can reference for node selection when deploying the CNPG operator later in this guide. This section might take some time to complete.

Important

If you opt to use local NVMe as your PostgreSQL storage in the later parts of this guide, you need to choose a VM SKU that supports local NVMe drives, for example, [Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized) or [GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). Update `$USER_NODE_POOL_VMSKU`

accordingly.

Create an AKS cluster using the

command.`az aks create`

`export SYSTEM_NODE_POOL_VMSKU="standard_d2s_v3" export USER_NODE_POOL_NAME="postgres" export USER_NODE_POOL_VMSKU="standard_d4s_v3" az aks create \ --name $AKS_PRIMARY_CLUSTER_NAME \ --tags $TAGS \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --generate-ssh-keys \ --node-resource-group $AKS_PRIMARY_MANAGED_RG_NAME \ --enable-managed-identity \ --assign-identity $AKS_UAMI_WORKLOAD_RESOURCEID \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --nodepool-name systempool \ --enable-oidc-issuer \ --enable-workload-identity \ --enable-cluster-autoscaler \ --min-count 2 \ --max-count 3 \ --node-vm-size $SYSTEM_NODE_POOL_VMSKU \ --enable-azure-monitor-metrics \ --azure-monitor-workspace-resource-id $AMW_RESOURCE_ID \ --grafana-resource-id $GRAFANA_RESOURCE_ID \ --api-server-authorized-ip-ranges $MY_PUBLIC_CLIENT_IP \ --tier standard \ --kubernetes-version $AKS_CLUSTER_VERSION \ --zones 1 2 3 \ --output table`

Wait for the initial cluster operation to complete using the

command so additional updates, such as adding the user node pool, don’t collide with an in-progress managed-cluster update:`az aks wait`

`az aks wait \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --created`

Add a user node pool to the AKS cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $AKS_PRIMARY_CLUSTER_NAME \ --name $USER_NODE_POOL_NAME \ --enable-cluster-autoscaler \ --min-count 3 \ --max-count 6 \ --node-vm-size $USER_NODE_POOL_VMSKU \ --zones 1 2 3 \ --labels workload=postgres \ --output table`


## Connect to the AKS cluster and create namespaces

In this section, you get the AKS cluster credentials, which serve as the keys that allow you to authenticate and interact with the cluster. Once connected, you create two namespaces: one for the CNPG controller manager services and one for the PostgreSQL cluster and its related services.

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --output none`

Create the namespace for the CNPG controller manager services, the PostgreSQL cluster, and its related services by using the

command.`kubectl create namespace`

`kubectl create namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME kubectl create namespace $PG_SYSTEM_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


You can now define another environment variable based on your desired storage option, which you reference later in the guide when deploying PostgreSQL.

You can reference the default preinstalled Premium SSD Azure Disks CSI driver storage class:

```
export POSTGRES_STORAGE_CLASS="managed-csi-premium"
```


## Update the monitoring infrastructure

The Azure Monitor workspace for Managed Prometheus and Azure Managed Grafana are automatically linked to the AKS cluster for metrics and visualization during the cluster creation process. In this section, you enable log collection with AKS Container insights and validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs.

Enable Container insights monitoring on the AKS cluster using the

command.`az aks enable-addons`

`az aks enable-addons \ --addon monitoring \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-resource-id $ALA_RESOURCE_ID \ --output table`

Validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs from the AKS cluster by inspecting the DaemonSet using the

command and the`kubectl get`

command.`az aks show`

`kubectl get ds ama-metrics-node \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system kubectl get ds ama-logs \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system az aks show \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --query addonProfiles`

Your output should resemble the following example output, with

*six*nodes total (three for the system node pool and three for the PostgreSQL node pool) and the Container insights showing`"enabled": true`

:`NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-metrics-node 6 6 6 6 6 <none> NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-logs 6 6 6 6 6 <none> { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/rg-cnpg-9vbin3p8/providers/Microsoft.OperationalInsights/workspaces/ala-cnpg-9vbin3p8", "useAADAuth": "true" }, "enabled": true, "identity": null } }`


## Create a public static IP for PostgreSQL cluster ingress

To validate deployment of the PostgreSQL cluster and use client PostgreSQL tooling, such as *psql* and *PgAdmin*, you need to expose the primary and read-only replicas to ingress. In this section, you create an Azure public IP resource that you later supply to an Azure load balancer to expose PostgreSQL endpoints for query.

Get the name of the AKS cluster node resource group using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME=$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query nodeResourceGroup \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME`

Create the public IP address using the

command.`az network public-ip create`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_NAME="$AKS_PRIMARY_CLUSTER_NAME-pip" az network public-ip create \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard \ --zone 1 2 3 \ --allocation-method static \ --output table`

Get the newly created public IP address using the

command.`az network public-ip show`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS=$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query ipAddress \ --output tsv) echo $AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS`

Get the resource ID of the node resource group using the

command.`az group show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE=$(az group show --name \ $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --query id \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE`

Assign the "Network Contributor" role to the UAMI object ID using the node resource group scope using the

command.`az role assignment create`

`az role assignment create \ --assignee-object-id ${AKS_UAMI_WORKLOAD_OBJECTID} \ --assignee-principal-type ServicePrincipal \ --role "Network Contributor" \ --scope ${AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE}`


## Install the CNPG operator in the AKS cluster

In this section, you install the CNPG operator in the AKS cluster using Helm or a YAML manifest.

Add the CNPG Helm repo using the

command.`helm repo add`

`helm repo add cnpg https://cloudnative-pg.github.io/charts`

Upgrade the CNPG Helm repo and install it on the AKS cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install cnpg \ --namespace $PG_SYSTEM_NAMESPACE \ --create-namespace \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME \ cnpg/cloudnative-pg`

Verify the operator installation on the AKS cluster using the

command.`kubectl get`

`kubectl get deployment \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_SYSTEM_NAMESPACE cnpg-cloudnative-pg`


## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-azure-rbac -->

# Use Azure role-based access control for Kubernetes Authorization

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers how to use Azure RBAC for Kubernetes Authorization, which allows for the unified management and access control across Azure resources, AKS, and Kubernetes resources. For more information, see [Azure RBAC for Kubernetes Authorization](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization).

Note

When using [integrated authentication between Microsoft Entra ID and AKS](managed-azure-ad), you can use Microsoft Entra users, groups, or service principals as subjects in [Kubernetes role-based access control (Kubernetes RBAC)](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization). With this feature, you don't need to separately manage user identities and credentials for Kubernetes. However, you still need to set up and manage Azure RBAC and Kubernetes RBAC separately.

## Before you begin

- You need the Azure CLI version 2.24.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

, with a minimum version of[1.18.3](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1183). - You need managed Microsoft Entra integration enabled on your cluster before you can add Azure RBAC for Kubernetes authorization. If you need to enable managed Microsoft Entra integration, see
[Use Microsoft Entra ID in AKS](managed-azure-ad). - If you have CRDs and are making custom role definitions, the only way to cover CRDs today is to use
`Microsoft.ContainerService/managedClusters/*/read`

. For the remaining objects, you can use the specific API groups, such as`Microsoft.ContainerService/apps/deployments/read`

. - New role assignments can take
*up to five minutes*to propagate and be updated by the authorization server. - Azure RBAC for Kubernetes Authorization requires that the Microsoft Entra tenant configured for authentication is same as the tenant for the subscription that holds your AKS cluster.

## Create a new AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization

Create an Azure resource group using the

command.`az group create`

`export RESOURCE_GROUP=<resource-group-name> export LOCATION=<azure-region> az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization using the

command.`az aks create`

`export CLUSTER_NAME=<cluster-name> az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-aad \ --enable-azure-rbac \ --generate-ssh-keys`

Your output should look similar to the following example output:

`"AADProfile": { "adminGroupObjectIds": null, "clientAppId": null, "enableAzureRbac": true, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "****-****-****-****-****" }`


## Enable Azure RBAC on an existing AKS cluster

Enable Azure RBAC for Kubernetes Authorization on an existing AKS cluster using the

command with the`az aks update`

`--enable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac`


## Disable Azure RBAC for Kubernetes Authorization from an AKS cluster

Remove Azure RBAC for Kubernetes Authorization from an existing AKS cluster using the

command with the`az aks update`

`--disable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --disable-azure-rbac`


## AKS built-in roles

AKS provides the following built-in roles:

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. It doesn't allow viewing roles or role bindings. This role doesn't allow viewing `Secrets` , since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. This role doesn't allow viewing or modifying roles or role bindings. However, this role allows accessing `Secrets` and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. This role doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. It gives full control over every resource in the cluster and in all namespaces. |

## Create role assignments for cluster access

Get your AKS resource ID using the

command.`az aks show`

`AKS_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query id --output tsv)`

Create a role assignment using the

command.`az role assignment create`

`<AAD-ENTITY-ID>`

can be a username or the client ID of a service principal. The following example creates a role assignment for the*Azure Kubernetes Service RBAC Admin*role.`az role assignment create --role "Azure Kubernetes Service RBAC Admin" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`

Note

You can create the

*Azure Kubernetes Service RBAC Reader*and*Azure Kubernetes Service RBAC Writer*role assignments scoped to a specific namespace within the cluster using thecommand and setting the scope to the desired namespace.`az role assignment create`

`az role assignment create --role "Azure Kubernetes Service RBAC Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID/namespaces/<namespace-name>`


## Create custom roles definitions

The following example custom role definition allows a user to only read deployments and nothing else. For the full list of possible actions, see [Microsoft.ContainerService operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftcontainerservice).

To create your own custom role definitions, copy the following file, replacing

`<YOUR SUBSCRIPTION ID>`

with your own subscription ID, and then save it as`deploy-view.json`

.`{ "Name": "AKS Deployment Reader", "Description": "Lets you view all deployments in cluster/namespace.", "Actions": [], "NotActions": [], "DataActions": [ "Microsoft.ContainerService/managedClusters/apps/deployments/read" ], "NotDataActions": [], "assignableScopes": [ "/subscriptions/<YOUR SUBSCRIPTION ID>" ] }`

Create the role definition using the

command, setting the`az role definition create`

`--role-definition`

to the`deploy-view.json`

file you created in the previous step.`az role definition create --role-definition @deploy-view.json`

Assign the role definition to a user or other identity using the

command.`az role assignment create`

`az role assignment create --role "AKS Deployment Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`


## Use Azure RBAC for Kubernetes Authorization with `kubectl`


Make sure you have the

[Azure Kubernetes Service Cluster User](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-user-role)built-in role, and then get the kubeconfig of your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Use Azure RBAC for Kubernetes Authorization with `kubelogin`


AKS created the [ kubelogin](https://github.com/Azure/kubelogin) plugin to help unblock scenarios such as non-interactive logins, older

`kubectl`

versions, or leveraging SSO across multiple clusters without the need to sign in to a new cluster.Use the

`kubelogin`

plugin by running the following command:`export KUBECONFIG=/path/to/kubeconfig kubelogin convert-kubeconfig`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Clean up resources

### Delete role assignment

List role assignments using the

command.`az role assignment list`

`az role assignment list --scope $AKS_ID --query [].id --output tsv`

Delete role assignments using the

command.`az role assignment delete`

`az role assignment delete --ids <LIST OF ASSIGNMENT IDS>`


### Delete role definition

Delete the custom role definition using the

command.`az role definition delete`

`az role definition delete --name "AKS Deployment Reader"`


### Delete resource group and AKS cluster

Delete the resource group and AKS cluster using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP --yes --no-wait`


## Next steps

To learn more about AKS authentication, authorization, Kubernetes RBAC, and Azure RBAC, see:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-cvm -->

# Use Confidential Virtual Machines (CVM) in Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Confidential Virtual Machines (CVM)](/en-us/azure/confidential-computing/confidential-vm-overview) offer strong security and confidentiality for tenants. CVMs offer VM based Hardware Trusted Execution Environment (TEE) that leverage SEV-SNP security features to deny the hypervisor and other host management code access to VM memory and state, providing defense in depth protections against operator access. These features enable node pools with CVM to target the migration of highly sensitive container workloads to AKS without any code refactoring while benefiting from the features of AKS. For example, you may require CVM if you have the following:

- Workloads that handle security critical data and/or sensitive customer data
- Services that are required to meet various compliance requirements, especially for government contracts. Without a scalable solution for securing data, this could potentially lead to the loss of accreditations and contracts.

In this article, you learn how to create AKS node pools using Confidential VM sizes.

## AKS supported confidential VM sizes

Azure offers a choice of [Trusted Execution Environment (TEE)](/en-us/azure/confidential-computing/trusted-execution-environment) options from both AMD and Intel. These TEEs allow you to create Confidential VM environments with excellent price-to-performance ratios, all without requiring any code changes.

- AMD-based Confidential VMs, use AMD SEV-SNP technology, which is introduced with third Gen AMD EPYC™ processors.
- Intel-based Confidential VMs use Intel TDX, with fourth Gen Intel® Xeon® processors.

Both technologies have different implementations. However both provide similar protections from the cloud infrastructure stack. For more information, see [CVM VM sizes](/en-us/azure/confidential-computing/virtual-machine-options).

## Security Features

CVMs offer the following security enhancements as compared to other virtual machine (VM) sizes:

- Robust hardware-based isolation between virtual machines, hypervisor, and host management code.
- Customizable attestation policies to ensure the host's compliance before deployment.
- Cloud-based Confidential OS disk encryption before the first boot.
- VM encryption keys that the platform or the customer (optionally) owns and manages.
- Secure key release with cryptographic binding between the platform's successful attestation and the VM's encryption keys.
- Dedicated virtual Trusted Platform Module (TPM) instance for attestation and protection of keys and secrets in the virtual machine.
- Secure boot capability similar to Trusted launch for Azure VMs

## How does it work?

If you're running a workload that requires enhanced confidentiality and integrity, you can benefit from memory encryption and enhanced security without code changes in your application. All pods on your CVM node are part of the same trust boundary. The nodes in a node pool created with CVM use a customized [node image](node-images) specially configured for CVM.

### Supported OS Versions

You can create CVM node pools on Linux OS types (Ubuntu and Azure Linux). However, not all OS versions support CVM node pools.

This table includes the supported OS versions:

| OS Type | OS SKU | CVM support | CVM default |
|---|---|---|---|
| Linux | `Ubuntu` |
Supported | Ubuntu 20.04 is default for K8s version 1.24-1.33. Ubuntu 24.04 is the default for K8s version 1.34-1.38. |
| Linux | `Ubuntu2204` |
Not Supported | AKS doesn't support CVM for Ubuntu 22.04. |
| Linux | `Ubuntu2404` |
Supported | CVM is supported on `Ubuntu2404` in K8s 1.32-1.38. |
| Linux | `AzureLinux` |
Supported on Azure Linux 3.0 | Azure Linux 3 is default when enabling CVM for K8s version 1.28-1.36. |
| Linux | `flatcar` |
Not supported |
|

`AzureLinuxOSGuard`

[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)doesn't support CVM.When using `Ubuntu`

or `AzureLinux`

as the `osSKU`

, if the default OS version doesn't support CVM, AKS defaults to the most recent CVM-supported version of the OS. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support CVM, AKS defaults to Ubuntu 20.04 for Linux CVM-enabled node pools.

### Limitations

The following limitations apply when adding a node pool with CVM to AKS:

- You can't use FIPS, ARM64, Trusted Launch, or Pod Sandboxing.
- You can't update an existing node pool to migrate to a CVM size. To migrate, you'll need to
[resize your node pool](resize-node-pool). - You can't use CVM with Windows node pools.
- CVM with Azure Linux is currently in preview.

## Prerequisites

Before you begin, make sure you have the following:

- An existing AKS cluster.
- CVM sizes must be available for your subscription in the region where the cluster is created. You must have sufficient quota to create a node pool with a CVM size.
- If you're using Azure Linux os, you need to install the
`aks-preview`

extension, update the`aks-preview`

extension, and register the preview feature flag. If you're using Ubuntu, you can skip these steps.

### If you are using Azure Linux

CVMs for Ubuntu is GA, but CVMs with Azure Linux is currently still in preview. If you would like to use CVM node pools with Azure Linux as the OS of choice, ensure you enable the extension and register the flag.

#### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


#### Register `AzureLinuxCVMPreview`

feature flag

Register the

`AzureLinuxCVMPreview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AzureLinuxCVMPreview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AzureLinuxCVMPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a node pool with a CVM to your AKS cluster

Add a node pool with a CVM to your AKS cluster using the

command and set the`az aks nodepool add`

`node-vm-size`

to a supported[VM size](/en-us/azure/confidential-computing/virtual-machine-options).`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --node-count 3 \ --node-vm-size Standard_DC4as_v5`


If you don't specify the `osSKU`

or `osType`

, AKS defaults to `--os-type Linux`

and `--os-sku Ubuntu`

.

## Upgrade an existing node pool with a CVM to Ubuntu 24.04

Upgrade an existing node pool with a CVM to Ubuntu 24.04 from Ubuntu 20.04 using the

command. Set the`az aks nodepool update`

`os-sku`

as`Ubuntu2404`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --os-sku Ubuntu2404`


Note

A node pool which is Ubuntu 24.04 with a CVM is supported from AKS cluster 1.33 version. Additionally, before Ubuntu 24.04 becomes GA, you need to register the `Ubuntu2404Preview`

feature. For more information, see [ here](/en-us/azure/aks/upgrade-os-version#register-ubuntu2404preview-feature-flag) to register the feature.

## Verify the node pool uses CVM

Verify a node pool uses CVM using the

command and verify the`az aks nodepool show`

`vmSize`

is`Standard_DCa4_v5`

.`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize'`

The following example command and output shows the node pool uses CVM:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize' "Standard_DC4as_v5"`

Verify a node pool uses a CVM image using the

command.`az aks nodepool list`

`az aks nodepool list \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion'`

The following example command and output shows the node pool uses an Ubuntu 20.04 CVM image:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion' "AKSUbuntu-2004cvmcontainerd-202507.02.0"`


## Remove a node pool with CVM from an AKS cluster

Remove a node pool with CVM from an AKS cluster using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool`


## Next steps

In this article, you learned how to add a node pool with CVM to an AKS cluster.

- For more information about CVM, see
[Confidential VM node pools support on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks). - To migrate an existing node pool to a CVM vm size, you can
[resize your node pool](resize-node-pool). - If you're only interested in enabling Trusted Launch on your node pools, see
[Trusted Launch on AKS](use-trusted-launch).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster -->

# Automatically upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Part of the AKS cluster lifecycle involves performing periodic upgrades to the latest Kubernetes version. It's important you apply the latest security releases or upgrade to get the latest features. Before you learn about automatic upgrades, make sure you understand the [AKS cluster upgrade fundamentals](upgrade-cluster).

Note

Any upgrade operation, whether performed manually or automatically, upgrades the node image version if it's not already on the latest version. The latest version is contingent on a full AKS release and can be determined by visiting the [AKS release tracker](release-tracker).

Autoupgrade first upgrades the control plane, and then upgrades agent pools one by one.

## Why use cluster autoupgrade

Cluster autoupgrade provides a *set once and forget* mechanism that yields tangible time and operational cost benefits. You don't need to stop your workloads, redeploy your workloads, or create a new AKS cluster. By enabling autoupgrade, you can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes.

AKS follows a strict supportability versioning window. With properly selected autoupgrade channels, you can avoid clusters falling into an unsupported version. For more on the AKS support window, see [Alias minor versions](supported-kubernetes-versions).

## Customer versus AKS-initiated autoupgrades

You can specify cluster autoupgrade specifics using the following guidance. The upgrades occur based on your specified cadence and are recommended to remain on supported Kubernetes versions.

AKS also initiates autoupgrades for unsupported clusters. When a cluster in an n-3 version (where n is the latest supported AKS GA minor version) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support [policy](supported-kubernetes-versions). Automatically upgrading a platform supported cluster to a supported version is enabled by default. Stopped node pools are upgraded during an autoupgrade operation. The upgrade applies to nodes when the node pool is started. To minimize disruptions, set up [maintenance windows](planned-maintenance).

## Cluster autoupgrade limitations

If you're using cluster autoupgrade, you can no longer upgrade the control plane first, and then upgrade the individual node pools. Cluster autoupgrade always upgrades the control plane and the node pools together. You can't upgrade the control plane only. Running the `az aks upgrade --control-plane-only`

command raises the following error:

```
NotAllAgentPoolOrchestratorVersionSpecifiedAndUnchanged: Using managed cluster api, all Agent pools' OrchestratorVersion must be all specified or all unspecified. If all specified, they must be stay unchanged or the same with control plane.
```


If using the `node-image`

(legacy and not to be used) cluster autoupgrade channel or the `NodeImage`

node image autoupgrade channel, Linux [unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates) are disabled by default.

## Cluster autoupgrade channels

Automatically completed upgrades are functionally the same as manual upgrades. The [selected autoupgrade channel](planned-maintenance) determines the timing of upgrades. When making changes to autoupgrade, allow 24 hours for the changes to take effect. Automatically upgrading a cluster follows the same process as manually upgrading a cluster. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

The following upgrade channels are available:

| Channel | Action | Example |
|---|---|---|
`none` |
disables autoupgrades and keeps the cluster at its current version of Kubernetes. | Default setting if left unchanged. |
`patch` |
automatically upgrades the cluster to the latest supported patch version when it becomes available while keeping the minor version the same. | For example, if a cluster runs version 1.17.7, and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.17.9. |
`stable` |
automatically upgrades the cluster to the latest supported patch release on minor version N-1, where N is the latest supported minor version. |
For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.18.6. |
`rapid` |
automatically upgrades the cluster to the latest supported patch release on the latest supported minor version. | In cases where the cluster's Kubernetes version is an N-2 minor version, where N is the latest supported minor version, the cluster first upgrades to the latest supported patch version on N-1 minor version. For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster first upgrades to 1.18.6, then upgrades to 1.19.1. |
`node-image` (legacy) |
automatically upgrades the node image to the latest version available. | Microsoft provides patches and new images for image nodes frequently (weekly), but your running nodes don't get the new images unless you do a node image upgrade. Turning on the node-image channel automatically updates your node images whenever a new version is available. If you use this channel, Linux [unattended upgrades] are disabled by default. Node image upgrades work on patch versions that are deprecated, so long as the minor Kubernetes version is still supported. This channel is no longer recommended and is planned for deprecation in future. For an option that can automatically upgrade node images, see the `NodeImage` channel in
|

Note

Keep the following information in mind when using cluster autoupgrade:

Cluster autoupgrade only updates to GA versions of Kubernetes and doesn't update to preview versions.

With AKS, you can create a cluster without specifying the exact patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. To learn more, see

[AKS support window](supported-kubernetes-versions).Autoupgrade requires the cluster's Kubernetes version to be within the

[AKS support window](supported-kubernetes-versions), even if using the`node-image`

channel.If you're using the preview API

`11-02-preview`

or later, and you select the`node-image`

cluster autoupgrade channel, the[node image autoupgrade channel](auto-upgrade-node-image)automatically sets to`NodeImage`

.Each cluster can only be associated with a single autoupgrade channel. The reason is because your specified channel determines the Kubernetes version that runs on the cluster.

If your cluster has no autoupgrade channel and you enable it for Long-Term Support (LTS), the cluster defaults to a

`patch`

autoupgrade channel.

## Use cluster autoupgrade with a new AKS cluster

Set the autoupgrade channel when creating a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and the

`auto-upgrade-channel`

parameter.```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster"
az aks create --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable --generate-ssh-keys
```


## Use cluster autoupgrade with an existing AKS cluster

Set the autoupgrade channel on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`auto-upgrade-channel`

parameter.```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable
```


Results:

```
{
"id": "/subscriptions/aaaa6a6a-bb7b-cc8c-dd9d-eeeeee0e0e0e/resourceGroups/myResourceGroupabc123/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
"properties": {
"autoUpgradeChannel": "stable",
"provisioningState": "Succeeded"
}
}
```


## Use autoupgrade with Planned Maintenance

If using Planned Maintenance and cluster autoupgrade, your upgrade starts during your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of *four hours or more*.

For more information on how to set a maintenance window with Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Best practices for cluster autoupgrade

Use the following best practices to help maximize your success when using autoupgrade:

- To ensure your cluster is always in a supported version, for example within the N-2 rule, choose either
`stable`

or`rapid`

channels. - If you're interested in getting the latest patches as soon as possible, use the
`patch`

channel. The`node-image`

channel is a good fit if you want your agent pools to always run the most recent node images. - To automatically upgrade node images while using a different cluster upgrade channel, consider using the
[node image autoupgrade](auto-upgrade-node-image)`NodeImage`

channel. - Follow
[Operator best practices](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets). - Follow
[PodDisruptionBudget (PDB) best practices](https://kubernetes.io/docs/tasks/run-application/configure-pdb/). - For upgrade troubleshooting information, see the
[AKS troubleshooting documentation](/en-us/support/azure/azure-kubernetes/welcome-azure-kubernetes).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-tool-calling -->

# Integrate tool calling with LLM Inference with the AI toolchain operator add-on on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS) with support for OpenAI-style tool calling. You also learn how to validate tool calling functionality using vLLM metrics and local function mocks.

## What is tool calling?

Tool calling enables large language models (LLMs) to interface with external functions, APIs, or services. Instead of just generating text, an LLM can decide:

- "I need to call a weather API."
- "I need to use a calculator."
- "I should search a database."

It does this by invoking a defined “tool” with parameters it chooses based on the user’s request. Tool calling is useful for:

- Chatbots that book, summarize, or calculate.
- Enterprise LLM applications where hallucination must be minimized.
- Agent frameworks (AutoGen, LangGraph, LangChain, AgentOps, etc.).

In production environments, AI-enabled applications often demand more than natural language generation; they require the ability to take action based on user intent. Tool calling empowers LLMs to extend beyond text responses by invoking external tools, APIs, or custom logic in real time. This bridges the gap between language understanding and execution, enabling developers to build interactive AI assistants, agents, and automation workflows that are both accurate and useful. Instead of relying on static responses, LLMs can now access live data, trigger services, and complete tasks on behalf of users, both safely and reliably.

When deployed on AKS, tool calling becomes scalable, secure, and production ready. Kubernetes provides the flexibility to orchestrate inference workloads using high-performance runtimes like vLLM, while ensuring observability and governance of tool usage. With this pattern, AKS operators and app developers can more seamlessly update models or tools independently and deploy advanced AI features without compromising reliability.

As a result, tool calling on AKS is now a foundational pattern for building modern AI apps that are context-aware, action-capable, and enterprise-ready.

### Tool calling with KAITO

To streamline this deployment model, the AI toolchain operator (KAITO) add-on for AKS provides a managed solution for running inference services with [tool calling support](https://kaito-project.github.io/kaito/docs/tool-calling/). By leveraging KAITO inference workspaces, you can quickly spin up scalable, GPU-accelerated model endpoints with built-in support for tool calling and OpenAI-compatible APIs. This eliminates the operational overhead of configuring runtimes, managing dependencies, or scaling infrastructure manually.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster. - A deployed KAITO inference workspace that supports tool calling. Refer to the official
[KAITO tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/)documentation for the tool calling supported models with vLLM. - You deployed the
`workspace‑phi‑4-mini-toolcall`

[KAITO workspace](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_tool_calling.yaml)with the default configuration.

## Confirm the KAITO inference workspace is running

Monitor your workspace deployment with the

`kubectl get`

command.`kubectl get workspace workspace‑phi‑4‑mini-toolcall -w`

In the output, you want to verify the resource (

`ResourceReady`

) and inference (`InferenceReady`

) are ready and the workspace succeeded (`WorkspaceSucceeded`

being`true`

).

## Confirm the inference API is ready to serve

Once the

[workspace is ready](#confirm-the-kaito-inference-workspace-is-running), find the service endpoint using the`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check the

`/v1/models`

endpoint to confirm the LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

To ensure the LLM is deployed, and the API is working, your output should be similar to the following:

`... { "object": "list", "data": [ { "id": "phi‑4‑mini‑instruct", ... ... } ] } ...`


## Test the named function tool‐calling

In this example, the `workspace‑phi‑4‑mini-toolcall`

workspace supports named function tool-calling by default, so we can confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure.

The Python snippet we use in this section is from the [KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/#examples) and uses an OpenAI‑compatible client.

Confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure. This example:

- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at
`http://localhost:8000/v1`

and accepts OpenAI-style API calls. - Simulates the backend logic for a tool called
`get_weather`

. (In a real scenario, this would call a weather API.) - Describes the tool interface; the
`Phi-4-mini`

LLM will see this tool and decide whether to use it based on the user's input. - Sends a sample chat message to the model and provides the tool spec. The setting
`tool_choice="auto"`

allows the LLM to decide if it should call a tool based on the prompt. - In this case, the user's request was relevant to the
`get_weather`

tool, so we simulate the execution of the tool, calling the local function with the model's chosen arguments.

`from openai import OpenAI import json # local server client = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy") def get_weather(location: str, unit: str) -> str: return f"Getting the weather for {location} in {unit}..." tool_functions = {"get_weather": get_weather} tools = [{ "type": "function", "function": { "name": "get_weather", "description": "Get the current weather in a given location", "parameters": { "type": "object", "properties": { "location": {"type": "string"}, "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]} }, "required": ["location", "unit"] } } }] response = client.chat.completions.create( model="phi‑4‑mini‑instruct", # or client.models.list().data[0].id messages=[{"role": "user", "content": "What's the weather like in San Francisco?"}], tools=tools, tool_choice="auto" ) # Inspect response tool_call = response.choices[0].message.tool_calls[0].function args = json.loads(tool_call.arguments) print("Function called:", tool_call.name) print("Arguments:", args) print("Result:", tool_functions[tool_call.name](**args))`

Your output should look similar to the following:

`Function called: get_weather Arguments: {"location": "San Francisco, CA", "unit": "fahrenheit"} Result: Getting the weather for San Francisco, CA in fahrenheit...`

The “tool_calls” field comes back, meaning the

`Phi-4-mini`

LLM decided to invoke the function. Now, a sample tool call has been successfully parsed and executed based on the model’s decision to confirm end-to-end tool calling behavior with the KAITO inference deployment.- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at

## Troubleshooting

### Model preset doesn’t support tool calling

If you pick a model that isn't on the supported list, tool calling might not work. Make sure you [review the KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/), which explicitly lists which presets support tool calling.

### Misaligned runtime

The KAITO inference must use [vLLM runtime for tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/#supported-inference-runtimes) (HuggingFace Transformers runtime generally doesn’t support tool calling in KAITO).

### Network / endpoint issues

If port-forwarding, ensure the service ports are correctly forwarded. If the external MCP server is unreachable, will error out.

### Timeouts

External MCP server calls might take time. Make sure the adapter or client timeout is sufficiently high.

### Authentication

If the external MCP server requires authentication (API key, header, etc.), ensure you supply correct credentials.

## Next steps

- Set up
[vLLM monitoring in the AI toolchain operator add-on](ai-toolchain-operator-monitoring)with Prometheus and Grafana on AKS. - Learn about
[MCP server support with KAITO](ai-toolchain-operator-mcp)and test standardized tool calling examples on your AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-telemetry -->

# Telemetry API for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Istio can [generate metrics, distributed traces, and access logs](https://istio.io/latest/docs/concepts/observability/) for all workloads in the mesh. The Istio-based service mesh add-on for Azure Kubernetes Service (AKS) provides telemetry customization options through the [shared MeshConfig](istio-meshconfig) and the Istio Telemetry API `v1`

for Istio add-on minor revisions `asm-1-22`

and higher.

Note

While the [Istio MeshConfig](istio-meshconfig) also provides options for configuring telemetry globally across the mesh, the Telemetry API offers more granular control over telemetry settings on a per-service or per-workload basis. As the Istio community continues to invest in the Telemetry API, it is now the preferred method for telemetry configuration. We encourage migrating to the Telemetry API for configuring telemetry to be collected in the mesh.

## Prerequisites

- You must be on revision
`asm-1-22`

or higher. For information on how to perform minor version upgrades, see the[Istio add-on upgrade documentation](istio-upgrade).

## Configure Telemetry resources

The following example demonstrates how Envoy access logging can be enabled across the mesh for the Istio add-on via the Telemetry API using `asm-1-22`

(adjust the revision as needed). For guidance on other Telemetry API customizations for the add-on, see the [Telemetry API support scope](#telemetry-api-support-scope) section and the [Istio documentation](https://istio.io/latest/docs/reference/config/telemetry/).

### Deploy sample applications

Label the namespace for sidecar injection:

```
kubectl label ns default istio.io/rev=asm-1-22
```


Deploy the `sleep`

application and set the `SOURCE_POD`

environment variable:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/sleep/sleep.yaml
export SOURCE_POD=$(kubectl get pod -l app=sleep -o jsonpath={.items..metadata.name})
```


Then, deploy the `httpbin`

application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/httpbin/httpbin.yaml
```


### Enable Envoy access logging with the Istio Telemetry API

Deploy the following Istio `v1`

Telemetry API resource to enable Envoy access logging for the entire mesh:

```
cat <<EOF | kubectl apply -n aks-istio-system -f -
apiVersion: telemetry.istio.io/v1
kind: Telemetry
metadata:
name: mesh-logging-default
spec:
accessLogging:
- providers:
- name: envoy
EOF
```


### Test access logs

Send a request from `sleep`

to `httpbin`

:

```
kubectl exec "$SOURCE_POD" -c sleep -- curl -sS -v httpbin:8000/status/418
```


Verify that access logs are visible for the `sleep`

pod:

```
kubectl logs -l app=sleep -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.690Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 12 11 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" outbound|8000||httpbin.default.svc.cluster.local 10.244.0.12:53336 10.0.112.220:8000 10.244.0.12:42360 - default
```


Now, verify that access logs are visible for the `httpbin`

pod:

```
kubectl logs -l app=httpbin -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.696Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 2 1 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" inbound|8080|| 127.0.0.6:55401 10.244.0.13:8080 10.244.0.12:53336 outbound_.8000_._.httpbin.default.svc.cluster.local default
```


## Telemetry API support scope

For the Istio service mesh add-on for AKS, Telemetry API fields are classified as `allowed`

, `supported`

, and `blocked`

values. For more information about the Istio add-on's support policy for features and mesh configurations, see the Istio add-on [support policy document](istio-support-policy#allowed-supported-and-blocked-customizations).

The following Telemetry API configurations are either `allowed`

or `supported`

for the Istio add-on. Any field not included in this table is `blocked`

.

Telemetry API Field |
Supported/Allowed |
Notes |
|---|---|---|
`accessLogging.match` |
Supported | - |
`accessLogging.disabled` |
Supported | - |
`accessLogging.providers` |
Allowed | The default `envoy` access log provider is supported. For a managed experience for log collection and querying, see
`allowed` but unsupported. |
`metrics.overrides` |
Supported | - |
`metrics.providers` |
Allowed | Metrics collection with
`allowed` but unsupported. |

`tracing.*`

`allowed`

but unsupported.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-scenarios-hub -->

# AKS upgrade scenarios: Choose your path

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrading Azure Kubernetes Service (AKS) clusters safely requires the right strategy for your specific situation. Use this hub to quickly identify your scenario and get targeted guidance.

## What this article covers

This decision hub helps you choose the right AKS upgrade approach based on:

- A quick scenario finder with time constraints and priorities.
- Emergency upgrade paths for critical security responses.
- A strategy matrix that compares downtime tolerance and complexity.
- Role-based guidance for site reliability engineers, database administrators, developers, and security teams.
- Decision trees for complex multi-environment setups.

This hub is best for first-time upgraders, teams that need to evaluate options, and complex environments that require tailored approaches.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-aks-cluster).

## Quick scenario finder

What's your primary concern? Select your answer from the following table.

| My priority | Time constraint | Go to |
|---|---|---|
| Zero production downtime | Upgrade needed within hours |
|

[Staged fleet upgrades](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)[Safe version intake](aks-production-upgrade-strategies#scenario-3-safe-kubernetes-version-intake)[Fast security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)[Stateful workload patterns](stateful-workload-upgrades)[Seamless architecture](aks-production-upgrade-strategies#scenario-5-application-architecture-for-seamless-upgrades)## Emergency upgrade (30-90 minutes)

If you need a critical security patch now, select a link for instructions:

**Immediate action:**[Automated security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)**With stateful workloads:**[Database safety patterns](stateful-workload-upgrades#emergency-upgrade-checklist)**Rollback ready:**[Quick recovery guide](aks-production-upgrade-strategies#emergency-rollback-procedures)

## Upgrade strategy matrix

Find your ideal approach based on business constraints.

| Downtime tolerance | Environment | Best strategy | Time investment |
|---|---|---|---|
| <2 minutes | Production | Blue-green deployment | 45-60 min |
| <30 seconds | Stateful apps | Ferris wheel pattern | 60-90 min |
| Planned window | Multi-environment | Staged fleet upgrade | 2-4 hours |
| Zero tolerance | Mission-critical | Application architecture | Ongoing |

## Key upgrade topics

### Core upgrade mechanics

### Production-ready strategies

[Scenario-based production upgrades](aks-production-upgrade-strategies)[Stateful workload upgrade patterns](stateful-workload-upgrades)[Cross-environment upgrade staging](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)

### Advanced topics

## Quick wins (5-15 minutes)

Immediate actions that you can take:

**Pre-upgrade health check:**Run[cluster diagnostics](aks-diagnostics).**Backup validation:**Verify your[disaster recovery](ha-dr-overview)setup.**Monitoring setup:**Enable[upgrade notifications](aks-communication-manager).**Team preparation:**Review[support policies](support-policies).

## Learning path

If you're new to AKS upgrades, follow this learning sequence:

**Learn:**Learn about[Kubernetes concepts](core-aks-concepts)and read the[Upgrade overview](upgrade-cluster).**Practice:**Take the tutorial on how to[upgrade an AKS cluster](tutorial-kubernetes-upgrade-cluster).**Production:**Use the[production strategies](aks-production-upgrade-strategies).**Optimize:**Find out about[stateful patterns](stateful-workload-upgrades).

## Pro tips

**Always test in nonproduction first:**Perform tests even for emergency patches.**Monitor during upgrades:**Set up[real-time alerts](aks-communication-manager).**Plan for rollback:**Have a tested recovery procedure.**Communicate with teams:**Coordinate with app owners during upgrades.

## Related content

- For more help, choose your scenario from the preceding options or start with
[Production upgrade strategies](aks-production-upgrade-strategies). - For more information, see
[AKS support options](aks-support-help)or the[Troubleshooting guide](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-azure-rbac -->

# Use Azure role-based access control for Kubernetes Authorization

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers how to use Azure RBAC for Kubernetes Authorization, which allows for the unified management and access control across Azure resources, AKS, and Kubernetes resources. For more information, see [Azure RBAC for Kubernetes Authorization](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization).

Note

When using [integrated authentication between Microsoft Entra ID and AKS](managed-azure-ad), you can use Microsoft Entra users, groups, or service principals as subjects in [Kubernetes role-based access control (Kubernetes RBAC)](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization). With this feature, you don't need to separately manage user identities and credentials for Kubernetes. However, you still need to set up and manage Azure RBAC and Kubernetes RBAC separately.

## Before you begin

- You need the Azure CLI version 2.24.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

, with a minimum version of[1.18.3](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1183). - You need managed Microsoft Entra integration enabled on your cluster before you can add Azure RBAC for Kubernetes authorization. If you need to enable managed Microsoft Entra integration, see
[Use Microsoft Entra ID in AKS](managed-azure-ad). - If you have CRDs and are making custom role definitions, the only way to cover CRDs today is to use
`Microsoft.ContainerService/managedClusters/*/read`

. For the remaining objects, you can use the specific API groups, such as`Microsoft.ContainerService/apps/deployments/read`

. - New role assignments can take
*up to five minutes*to propagate and be updated by the authorization server. - Azure RBAC for Kubernetes Authorization requires that the Microsoft Entra tenant configured for authentication is same as the tenant for the subscription that holds your AKS cluster.

## Create a new AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization

Create an Azure resource group using the

command.`az group create`

`export RESOURCE_GROUP=<resource-group-name> export LOCATION=<azure-region> az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization using the

command.`az aks create`

`export CLUSTER_NAME=<cluster-name> az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-aad \ --enable-azure-rbac \ --generate-ssh-keys`

Your output should look similar to the following example output:

`"AADProfile": { "adminGroupObjectIds": null, "clientAppId": null, "enableAzureRbac": true, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "****-****-****-****-****" }`


## Enable Azure RBAC on an existing AKS cluster

Enable Azure RBAC for Kubernetes Authorization on an existing AKS cluster using the

command with the`az aks update`

`--enable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac`


## Disable Azure RBAC for Kubernetes Authorization from an AKS cluster

Remove Azure RBAC for Kubernetes Authorization from an existing AKS cluster using the

command with the`az aks update`

`--disable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --disable-azure-rbac`


## AKS built-in roles

AKS provides the following built-in roles:

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. It doesn't allow viewing roles or role bindings. This role doesn't allow viewing `Secrets` , since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. This role doesn't allow viewing or modifying roles or role bindings. However, this role allows accessing `Secrets` and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. This role doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. It gives full control over every resource in the cluster and in all namespaces. |

## Create role assignments for cluster access

Get your AKS resource ID using the

command.`az aks show`

`AKS_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query id --output tsv)`

Create a role assignment using the

command.`az role assignment create`

`<AAD-ENTITY-ID>`

can be a username or the client ID of a service principal. The following example creates a role assignment for the*Azure Kubernetes Service RBAC Admin*role.`az role assignment create --role "Azure Kubernetes Service RBAC Admin" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`

Note

You can create the

*Azure Kubernetes Service RBAC Reader*and*Azure Kubernetes Service RBAC Writer*role assignments scoped to a specific namespace within the cluster using thecommand and setting the scope to the desired namespace.`az role assignment create`

`az role assignment create --role "Azure Kubernetes Service RBAC Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID/namespaces/<namespace-name>`


## Create custom roles definitions

The following example custom role definition allows a user to only read deployments and nothing else. For the full list of possible actions, see [Microsoft.ContainerService operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftcontainerservice).

To create your own custom role definitions, copy the following file, replacing

`<YOUR SUBSCRIPTION ID>`

with your own subscription ID, and then save it as`deploy-view.json`

.`{ "Name": "AKS Deployment Reader", "Description": "Lets you view all deployments in cluster/namespace.", "Actions": [], "NotActions": [], "DataActions": [ "Microsoft.ContainerService/managedClusters/apps/deployments/read" ], "NotDataActions": [], "assignableScopes": [ "/subscriptions/<YOUR SUBSCRIPTION ID>" ] }`

Create the role definition using the

command, setting the`az role definition create`

`--role-definition`

to the`deploy-view.json`

file you created in the previous step.`az role definition create --role-definition @deploy-view.json`

Assign the role definition to a user or other identity using the

command.`az role assignment create`

`az role assignment create --role "AKS Deployment Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`


## Use Azure RBAC for Kubernetes Authorization with `kubectl`


Make sure you have the

[Azure Kubernetes Service Cluster User](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-user-role)built-in role, and then get the kubeconfig of your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Use Azure RBAC for Kubernetes Authorization with `kubelogin`


AKS created the [ kubelogin](https://github.com/Azure/kubelogin) plugin to help unblock scenarios such as non-interactive logins, older

`kubectl`

versions, or leveraging SSO across multiple clusters without the need to sign in to a new cluster.Use the

`kubelogin`

plugin by running the following command:`export KUBECONFIG=/path/to/kubeconfig kubelogin convert-kubeconfig`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Clean up resources

### Delete role assignment

List role assignments using the

command.`az role assignment list`

`az role assignment list --scope $AKS_ID --query [].id --output tsv`

Delete role assignments using the

command.`az role assignment delete`

`az role assignment delete --ids <LIST OF ASSIGNMENT IDS>`


### Delete role definition

Delete the custom role definition using the

command.`az role definition delete`

`az role definition delete --name "AKS Deployment Reader"`


### Delete resource group and AKS cluster

Delete the resource group and AKS cluster using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP --yes --no-wait`


## Next steps

To learn more about AKS authentication, authorization, Kubernetes RBAC, and Azure RBAC, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-postgresql-ha -->

# Create infrastructure for deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create the infrastructure resources needed to deploy a highly available PostgreSQL database on AKS using the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- Review the deployment overview and make sure you meet all the prerequisites in
[How to deploy a highly available PostgreSQL database on AKS with Azure CLI](postgresql-ha-overview). [Set environment variables](#set-environment-variables)for use throughout this guide.[Install the required extensions](#install-required-extensions).

## Set environment variables

Set the following environment variables for use throughout this guide:

```
export SUFFIX=$(cat /dev/urandom | LC_ALL=C tr -dc 'a-z0-9' | fold -w 8 | head -n 1)
export LOCAL_NAME="cnpg"
export TAGS="owner=user"
export RESOURCE_GROUP_NAME="rg-${LOCAL_NAME}-${SUFFIX}"
export PRIMARY_CLUSTER_REGION="canadacentral"
export AKS_PRIMARY_CLUSTER_NAME="aks-primary-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_MANAGED_RG_NAME="rg-${LOCAL_NAME}-primary-aksmanaged-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME="pg-primary-fedcred1-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_PG_DNSPREFIX=$(echo $(echo "a$(openssl rand -hex 5 | cut -c1-11)"))
export AKS_UAMI_CLUSTER_IDENTITY_NAME="mi-aks-${LOCAL_NAME}-${SUFFIX}"
export AKS_CLUSTER_VERSION="1.32"
export PG_NAMESPACE="cnpg-database"
export PG_SYSTEM_NAMESPACE="cnpg-system"
export PG_PRIMARY_CLUSTER_NAME="pg-primary-${LOCAL_NAME}-${SUFFIX}"
export PG_PRIMARY_STORAGE_ACCOUNT_NAME="hacnpgpsa${SUFFIX}"
export PG_STORAGE_BACKUP_CONTAINER_NAME="backups"
export MY_PUBLIC_CLIENT_IP=$(dig +short myip.opendns.com @resolver3.opendns.com)
```


## Install required extensions

Install the extensions needed for Kubernetes integration and monitoring:

```
az extension add --upgrade --name k8s-extension --yes
az extension add --upgrade --name amg --yes
```


As a prerequisite for using `kubectl`

, you need to first install [Krew](https://krew.sigs.k8s.io/), followed by the installation of the [CNPG plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). These installations enable the management of the PostgreSQL operator using the subsequent commands.

```
(
set -x; cd "$(mktemp -d)" &&
OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
KREW="krew-${OS}_${ARCH}" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
tar zxvf "${KREW}.tar.gz" &&
./"${KREW}" install krew
)
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
kubectl krew install cnpg
```


## Create a resource group

Create a resource group to hold the resources you create in this guide using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create \
--name $RESOURCE_GROUP_NAME \
--location $PRIMARY_CLUSTER_REGION \
--tags $TAGS \
--query 'properties.provisioningState' \
--output tsv
```


## Create a user-assigned managed identity

In this section, you create a user-assigned managed identity (UAMI) to allow the CNPG PostgreSQL to use an AKS workload identity to access Azure Blob Storage. This configuration allows the PostgreSQL cluster on AKS to connect to Azure Blob Storage without a secret.

Create a user-assigned managed identity using the

command.`az identity create`

`AKS_UAMI_WI_IDENTITY=$(az identity create \ --name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --output json)`

Enable AKS workload identity and generate a service account to use later in this guide using the following commands:

`export AKS_UAMI_WORKLOAD_OBJECTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.principalId') export AKS_UAMI_WORKLOAD_RESOURCEID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.id') export AKS_UAMI_WORKLOAD_CLIENTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.clientId') echo "ObjectId: $AKS_UAMI_WORKLOAD_OBJECTID" echo "ResourceId: $AKS_UAMI_WORKLOAD_RESOURCEID" echo "ClientId: $AKS_UAMI_WORKLOAD_CLIENTID"`


The object ID is a unique identifier for the client ID (also known as the application ID) that uniquely identifies a security principal of type *Application* within the Microsoft Entra ID tenant. The resource ID is a unique identifier to manage and locate a resource in Azure. These values are required to enabled AKS workload identity.

The CNPG operator automatically generates a service account called *postgres* that you use later in the guide to create a federated credential that enables OAuth access from PostgreSQL to Azure Storage.

## Create a storage account in the primary region

Create an object storage account to store PostgreSQL backups in the primary region using the

command.`az storage account create`

`az storage account create \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard_ZRS \ --kind StorageV2 \ --query 'provisioningState' \ --output tsv`

Create the storage container to store the Write Ahead Logs (WAL) and regular PostgreSQL on-demand and scheduled backups using the

command.`az storage container create`

`az storage container create \ --name $PG_STORAGE_BACKUP_CONTAINER_NAME \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --auth-mode login`

Example output:

`{ "created": true }`

Note

If you encounter the error message:

`The request may be blocked by network rules of storage account. Please check network rule set using 'az storage account show -n accountname --query networkRuleSet'. If you want to change the default action to apply when no rule matches, please use 'az storage account update'`

. Make sure to verify user permissions for Azure Blob Storage and, if**necessary**, elevate your role to`Storage Blob Data Owner`

using the commands provided and after retry thecommand.`az storage container create`

`export USER_ID=$(az ad signed-in-user show --query id --output tsv) export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) az role assignment list --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID --output table az role assignment create \ --assignee-object-id $USER_ID \ --assignee-principal-type User \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --role "Storage Blob Data Owner" \ --output tsv`


## Assign RBAC to storage accounts

To enable backups, the PostgreSQL cluster needs to read and write to an object store. The PostgreSQL cluster running on AKS uses a workload identity to access the storage account via the CNPG operator configuration parameter [ inheritFromAzureAD](https://cloudnative-pg.io/documentation/1.23/appendixes/object_stores/#azure-blob-storage).

Get the primary resource ID for the storage account using the

command.`az storage account show`

`export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) echo $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID`

Assign the "Storage Blob Data Contributor" Azure built-in role to the object ID with the storage account resource ID scope for the UAMI associated with the managed identity for each AKS cluster using the

command.`az role assignment create`

`az role assignment create \ --role "Storage Blob Data Contributor" \ --assignee-object-id $AKS_UAMI_WORKLOAD_OBJECTID \ --assignee-principal-type ServicePrincipal \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --query "id" \ --output tsv`


## Set up monitoring infrastructure

In this section, you deploy an instance of Azure Managed Grafana, an Azure Monitor workspace, and an Azure Monitor Log Analytics workspace to enable monitoring of the PostgreSQL cluster. You also store references to the created monitoring infrastructure to use as input during the AKS cluster creation process later in the guide. This section might take some time to complete.

Note

Azure Managed Grafana instances and AKS clusters are billed independently. For more pricing information, see [Azure Managed Grafana pricing](https://azure.microsoft.com/pricing/details/managed-grafana/).

Create an Azure Managed Grafana instance using the

command.`az grafana create`

`export GRAFANA_PRIMARY="grafana-${LOCAL_NAME}-${SUFFIX}" export GRAFANA_RESOURCE_ID=$(az grafana create \ --resource-group $RESOURCE_GROUP_NAME \ --name $GRAFANA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --zone-redundancy Enabled \ --tags $TAGS \ --query "id" \ --output tsv) echo $GRAFANA_RESOURCE_ID`

Create an Azure Monitor workspace using the

command.`az monitor account create`

`export AMW_PRIMARY="amw-${LOCAL_NAME}-${SUFFIX}" export AMW_RESOURCE_ID=$(az monitor account create \ --name $AMW_PRIMARY \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --tags $TAGS \ --query "id" \ --output tsv) echo $AMW_RESOURCE_ID`

Create an Azure Monitor Log Analytics workspace using the

command.`az monitor log-analytics workspace create`

`export ALA_PRIMARY="ala-${LOCAL_NAME}-${SUFFIX}" export ALA_RESOURCE_ID=$(az monitor log-analytics workspace create \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-name $ALA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --query "id" \ --output tsv) echo $ALA_RESOURCE_ID`


## Create the AKS cluster to host the PostgreSQL cluster

In this section, you create a multizone AKS cluster with a system node pool. The AKS cluster hosts the PostgreSQL cluster primary replica and two standby replicas, each aligned to a different availability zone to enable zonal redundancy.

You also add a user node pool to the AKS cluster to host the PostgreSQL cluster. Using a separate node pool allows for control over the Azure VM SKUs used for PostgreSQL and enables the AKS system pool to optimize performance and costs. You apply a label to the user node pool that you can reference for node selection when deploying the CNPG operator later in this guide. This section might take some time to complete.

Important

If you opt to use local NVMe as your PostgreSQL storage in the later parts of this guide, you need to choose a VM SKU that supports local NVMe drives, for example, [Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized) or [GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). Update `$USER_NODE_POOL_VMSKU`

accordingly.

Create an AKS cluster using the

command.`az aks create`

`export SYSTEM_NODE_POOL_VMSKU="standard_d2s_v3" export USER_NODE_POOL_NAME="postgres" export USER_NODE_POOL_VMSKU="standard_d4s_v3" az aks create \ --name $AKS_PRIMARY_CLUSTER_NAME \ --tags $TAGS \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --generate-ssh-keys \ --node-resource-group $AKS_PRIMARY_MANAGED_RG_NAME \ --enable-managed-identity \ --assign-identity $AKS_UAMI_WORKLOAD_RESOURCEID \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --nodepool-name systempool \ --enable-oidc-issuer \ --enable-workload-identity \ --enable-cluster-autoscaler \ --min-count 2 \ --max-count 3 \ --node-vm-size $SYSTEM_NODE_POOL_VMSKU \ --enable-azure-monitor-metrics \ --azure-monitor-workspace-resource-id $AMW_RESOURCE_ID \ --grafana-resource-id $GRAFANA_RESOURCE_ID \ --api-server-authorized-ip-ranges $MY_PUBLIC_CLIENT_IP \ --tier standard \ --kubernetes-version $AKS_CLUSTER_VERSION \ --zones 1 2 3 \ --output table`

Wait for the initial cluster operation to complete using the

command so additional updates, such as adding the user node pool, don’t collide with an in-progress managed-cluster update:`az aks wait`

`az aks wait \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --created`

Add a user node pool to the AKS cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $AKS_PRIMARY_CLUSTER_NAME \ --name $USER_NODE_POOL_NAME \ --enable-cluster-autoscaler \ --min-count 3 \ --max-count 6 \ --node-vm-size $USER_NODE_POOL_VMSKU \ --zones 1 2 3 \ --labels workload=postgres \ --output table`


## Connect to the AKS cluster and create namespaces

In this section, you get the AKS cluster credentials, which serve as the keys that allow you to authenticate and interact with the cluster. Once connected, you create two namespaces: one for the CNPG controller manager services and one for the PostgreSQL cluster and its related services.

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --output none`

Create the namespace for the CNPG controller manager services, the PostgreSQL cluster, and its related services by using the

command.`kubectl create namespace`

`kubectl create namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME kubectl create namespace $PG_SYSTEM_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


You can now define another environment variable based on your desired storage option, which you reference later in the guide when deploying PostgreSQL.

You can reference the default preinstalled Premium SSD Azure Disks CSI driver storage class:

```
export POSTGRES_STORAGE_CLASS="managed-csi-premium"
```


## Update the monitoring infrastructure

The Azure Monitor workspace for Managed Prometheus and Azure Managed Grafana are automatically linked to the AKS cluster for metrics and visualization during the cluster creation process. In this section, you enable log collection with AKS Container insights and validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs.

Enable Container insights monitoring on the AKS cluster using the

command.`az aks enable-addons`

`az aks enable-addons \ --addon monitoring \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-resource-id $ALA_RESOURCE_ID \ --output table`

Validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs from the AKS cluster by inspecting the DaemonSet using the

command and the`kubectl get`

command.`az aks show`

`kubectl get ds ama-metrics-node \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system kubectl get ds ama-logs \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system az aks show \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --query addonProfiles`

Your output should resemble the following example output, with

*six*nodes total (three for the system node pool and three for the PostgreSQL node pool) and the Container insights showing`"enabled": true`

:`NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-metrics-node 6 6 6 6 6 <none> NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-logs 6 6 6 6 6 <none> { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/rg-cnpg-9vbin3p8/providers/Microsoft.OperationalInsights/workspaces/ala-cnpg-9vbin3p8", "useAADAuth": "true" }, "enabled": true, "identity": null } }`


## Create a public static IP for PostgreSQL cluster ingress

To validate deployment of the PostgreSQL cluster and use client PostgreSQL tooling, such as *psql* and *PgAdmin*, you need to expose the primary and read-only replicas to ingress. In this section, you create an Azure public IP resource that you later supply to an Azure load balancer to expose PostgreSQL endpoints for query.

Get the name of the AKS cluster node resource group using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME=$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query nodeResourceGroup \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME`

Create the public IP address using the

command.`az network public-ip create`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_NAME="$AKS_PRIMARY_CLUSTER_NAME-pip" az network public-ip create \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard \ --zone 1 2 3 \ --allocation-method static \ --output table`

Get the newly created public IP address using the

command.`az network public-ip show`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS=$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query ipAddress \ --output tsv) echo $AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS`

Get the resource ID of the node resource group using the

command.`az group show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE=$(az group show --name \ $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --query id \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE`

Assign the "Network Contributor" role to the UAMI object ID using the node resource group scope using the

command.`az role assignment create`

`az role assignment create \ --assignee-object-id ${AKS_UAMI_WORKLOAD_OBJECTID} \ --assignee-principal-type ServicePrincipal \ --role "Network Contributor" \ --scope ${AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE}`


## Install the CNPG operator in the AKS cluster

In this section, you install the CNPG operator in the AKS cluster using Helm or a YAML manifest.

Add the CNPG Helm repo using the

command.`helm repo add`

`helm repo add cnpg https://cloudnative-pg.github.io/charts`

Upgrade the CNPG Helm repo and install it on the AKS cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install cnpg \ --namespace $PG_SYSTEM_NAMESPACE \ --create-namespace \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME \ cnpg/cloudnative-pg`

Verify the operator installation on the AKS cluster using the

command.`kubectl get`

`kubectl get deployment \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_SYSTEM_NAMESPACE cnpg-cloudnative-pg`


## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/http-proxy -->

# HTTP proxy support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to configure Azure Kubernetes Service (AKS) clusters to use an HTTP proxy for outbound internet access.

AKS clusters deployed into managed or custom virtual networks have certain outbound dependencies that are necessary to function properly, which created problems in environments requiring internet access to be routed through HTTP proxies. Nodes had no way of bootstrapping the configuration, environment variables, and certificates necessary to access internet services.

The HTTP proxy feature adds HTTP proxy support to AKS clusters, exposing a straightforward interface that you can use to secure AKS-required network traffic in proxy-dependent environments. With this feature, both AKS nodes and pods are configured to use the HTTP proxy. The feature also enables installation of a trusted certificate authority onto the nodes as part of bootstrapping a cluster. More complex solutions might require creating a chain of trust to establish secure communications across the network.

## Limitations and considerations

The following scenarios are **not** supported:

- Different proxy configurations per node pool
- User/Password authentication
- Custom certificate authorities (CAs) for API server communication
- AKS clusters with Windows node pools
- Node pools using Virtual Machine Availability Sets (VMAS)
- Using * as wildcard attached to a domain suffix for noProxy

`httpProxy`

, `httpsProxy`

, and `trustedCa`

have no value by default. Pods are injected with the following environment variables:

`HTTP_PROXY`

`http_proxy`

`HTTPS_PROXY`

`https_proxy`

`NO_PROXY`

`no_proxy`


To disable the injection of the proxy environment variables, you need to annotate the Pod with `"kubernetes.azure.com/no-http-proxy-vars":"true"`

.

## Before you begin

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a configuration file with HTTP proxy values

Create a file and provide values for `httpProxy`

, `httpsProxy`

, and `noProxy`

. If your environment requires it, provide a value for `trustedCa`

.

The schema for the config file looks like this:

```
{
"httpProxy": "string",
"httpsProxy": "string",
"noProxy": [
"string"
],
"trustedCa": "string"
}
```


Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate **must** support `Subject Alternative Names(SANs)`

instead of the deprecated Common Name certs.

There are differences in applications on how to comply with the environment variable `http_proxy`

, `https_proxy`

, and `no_proxy`

. Curl and Python don't support CIDR in `no_proxy`

, but Ruby does.

Example input:

```
{
"httpProxy": "http://myproxy.server.com:8080",
"httpsProxy": "https://myproxy.server.com:8080",
"noProxy": [
"localhost",
"127.0.0.1"
],
"trustedCA": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUgvVENDQmVXZ0F3SUJB...S0tLS0="
}
```


## Create a cluster with an HTTP proxy configuration using the Azure CLI

You can configure an AKS cluster with an HTTP proxy configuration during cluster creation.

Use the

command and pass in your configuration as a JSON file.`az aks create`

`az aks create \ --name $clusterName \ --resource-group $resourceGroup \ --http-proxy-config aks-proxy-config.json \ --generate-ssh-keys`

Your cluster should initialize with the HTTP proxy configured on the nodes.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update a cluster to update or enable HTTP proxy

Enable or update HTTP proxy configurations on an existing cluster using the

command.`az aks update`

For example, let's say you created a new file with the base64 encoded string of the new CA cert called

*aks-proxy-config-2.json*. You can update the proxy configuration on your cluster with the following command:`az aks update --name $clusterName --resource-group $resourceGroup --http-proxy-config aks-proxy-config-2.json`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster (Preview)

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy (preview)

Update your cluster to disable HTTP proxy using the

command with`az aks update`

`--disable-http-proxy`

flag.`az aks update --name $clusterName --resource-group $resourceGroup --disable-http-proxy`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating the HTTP proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, the proxy configuration is saved in the database but the proxy variables are removed from the pods and nodes.

To re-enable HTTP proxy on an existing cluster, use the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-http-proxy`

flag.```
az aks update --name $clusterName --resource-group $resourceGroup --enable-http-proxy
```


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Important

If you had an HTTP proxy configuration on your cluster before disabling, the existing HTTP proxy configuration automatically applies when you re-enable HTTP proxy on that cluster. We recommend verifying the configuration to ensure it meets your current requirements before proceeding. If you want to change your HTTP proxy configuration after re-enabling HTTP proxy, follow the steps to [Update the HTTP proxy configuration on an existing cluster](#update-a-cluster-to-update-or-enable-http-proxy).

## Configure an HTTP proxy configuration using an Azure Resource Manager (ARM) template

You can deploy an AKS cluster with an HTTP proxy using an ARM template.

Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate

**must**support`Subject Alternative Names (SANs)`

instead of the deprecated Common Name certs.There are differences in applications on how to comply with the environment variable

`http_proxy`

,`https_proxy`

, and`no_proxy`

. Curl and Python don't support CIDR in`no_proxy`

, but Ruby does.Create a template with HTTP proxy parameters. In your template, provide values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the HTTP Proxy configuration. Your cluster should initialize with your HTTP proxy configured on the nodes.


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update an ARM template to configure HTTP proxy

In your template, provide new values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

.The same schema used for CLI deployment exists in the

`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the updated HTTP Proxy configuration.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster using an ARM template (Preview)

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy

Update your cluster ARM template to disable HTTP proxy by setting

`enabled`

to`false`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "false", } }`

Deploy your ARM template with HTTP Proxy disabled.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating that the HTTP Proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, you can no longer add HTTP proxy configurations to that cluster.

If you want to re-enable HTTP proxy, follow the steps to [Update an HTTP proxy configuration using an ARM template](#update-an-arm-template-to-configure-http-proxy).

## Istio add-on HTTP proxy for External Services

If you're using the [Istio-based service mesh add-on for AKS](istio-about), you must create a Service Entry to enable your applications in the mesh to access noncluster or external resources via the HTTP proxy.

For example:

```
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: proxy
spec:
hosts:
- my-company-proxy.com # ignored
addresses:
- $PROXY_IP/32
ports:
- number: $PROXY_PORT
name: tcp
protocol: TCP
location: MESH_EXTERNAL
```


Create a file and provide values for

`PROXY_IP`

and`PROXY_PORT`

.You can deploy the Service Entry using:

`kubectl apply -f service_proxy.yaml`


## Monitoring add-on configuration

HTTP proxy with the monitoring add-on supports the following configurations:

- Outbound proxy without authentication
- Outbound proxy with trusted cert for Log Analytics endpoint

The following configuration isn't supported:

- Custom Metrics and Recommended Alerts features when using a proxy with trusted certificates

## Next steps

For more information regarding the network requirements of AKS clusters, see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).
