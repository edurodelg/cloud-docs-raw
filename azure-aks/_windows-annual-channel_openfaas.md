---
merged_at: 2026-01-25T12:25:33.919384
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-annual-channel.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-annual-channel -->

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

<!-- DOCUMENTO FUSIONADO: openfaas.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/openfaas -->

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
