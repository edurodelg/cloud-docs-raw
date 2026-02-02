---
merged_at: 2026-02-02T16:24:03.292025
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/how-to-create-function-azure-cli -->

# Quickstart: Create a function in Azure from the command line

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use local command-line tools to create a function that responds to HTTP requests. After verifying your code locally, you deploy it to a serverless Flex Consumption hosting plan in Azure Functions.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - The
`JAVA_HOME`

environment variable must be set to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

The

, used to parse JSON output, and is also available in Azure Cloud Shell.`jq`

command line JSON processor

## Install the Azure Functions Core Tools

The recommended way to install Core Tools depends on the operating system of your local development computer.

The following steps use a Windows installer (MSI) to install Core Tools v4.x. For more information about other package-based installers, see the [Core Tools readme](https://github.com/Azure/azure-functions-core-tools/blob/v4.x/README.md#windows).

Download and run the Core Tools installer, based on your version of Windows:

[v4.x - Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2174087)(Recommended.[Visual Studio Code debugging](functions-develop-vs-code#debugging-functions-locally)requires 64-bit.)[v4.x - Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2174159)

If you previously used Windows installer (MSI) to install Core Tools on Windows, you should uninstall the old version from Add Remove Programs before installing the latest version.

Tip

To install Core Tools on [Windows Subsystem for Linux (WSL)](/en-us/windows/wsl/install), follow the instructions on the Linux tab.

## Create and activate a virtual environment

In a suitable folder, run the following commands to create and activate a virtual environment named `.venv`

. Make sure to use one of the [Python versions](functions-reference-python#supported-python-versions) supported by Azure Functions.

```
python -m venv .venv
```


```
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment.

## Create a local code project and function

In Azure Functions, your code project is an app that contains one or more individual functions that each respond to a specific trigger. All functions in a project share the same configurations and are deployed as a unit to Azure. In this section, you create a code project that contains a single function.

In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime dotnet-isolated`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime node --language javascript`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime powershell`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime python`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime node --language typescript`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime custom`


In an empty folder, run this

`mvn`

command to generate the code project from an Azure Functions[Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):`mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=17`

Important

- Use
`-DjavaVersion=11`

if you want your functions to run on Java 11. To learn more, see[Java versions](functions-reference-java#java-versions). - Set the
`JAVA_HOME`

environment variable to the install location of the correct version of the JDK to complete this article.

- Use
Maven asks you for values needed to finish generating the project on deployment.


Provide the following values when prompted:Prompt Value Description **groupId**`com.fabrikam`

A value that uniquely identifies your project across all projects, following the [package naming rules](https://docs.oracle.com/javase/specs/jls/se6/html/packages.html#7.7)for Java.**artifactId**`fabrikam-functions`

A value that is the name of the jar, without a version number. **version**`1.0-SNAPSHOT`

Choose the default value. **package**`com.fabrikam`

A value that is the Java package for the generated function code. Use the default. Type

`Y`

or press Enter to confirm.Maven creates the project files in a new folder with a name of

*artifactId*, which in this example is`fabrikam-functions`

.Navigate into the project folder:

`cd fabrikam-functions`

You can review the template-generated code for your new HTTP trigger function in

*Function.java*in the*\src\main\java\com\fabrikam*project directory.

Use this

command to add a function to your project:`func new`

`func new --name HttpExample --template "HTTP trigger" --authlevel "function"`

A new code file is added to your project. In this case, the

`--name`

argument is the unique name of your function (`HttpExample`

) and the`--template`

argument specifies an HTTP trigger.

The project root folder contains various files for the project, including configurations files named [local.settings.json](functions-develop-local#local-settings-file) and [host.json](functions-host-json). Because *local.settings.json* can contain secrets downloaded from Azure, the file is excluded from source control by default in the *.gitignore* file.

## Create and build your function

The *function.json* file in the *HttpExample* folder declares an HTTP trigger function. You complete the function by adding a handler and compiling it into an executable.

Press

`Ctrl + N`(`Cmd + N`on macOS) to create a new file. Save it as*handler.go*in the function app root (in the same folder as*host.json*).In

*handler.go*, add the following code and save the file. This is your Go custom handler.`package main import ( "fmt" "log" "net/http" "os" ) func helloHandler(w http.ResponseWriter, r *http.Request) { message := "This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response.\n" name := r.URL.Query().Get("name") if name != "" { message = fmt.Sprintf("Hello, %s. This HTTP triggered function executed successfully.\n", name) } fmt.Fprint(w, message) } func main() { listenAddr := ":8080" if val, ok := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT"); ok { listenAddr = ":" + val } http.HandleFunc("/api/HttpExample", helloHandler) log.Printf("About to listen on %s. Go to https://127.0.0.1%s/", listenAddr, listenAddr) log.Fatal(http.ListenAndServe(listenAddr, nil)) }`

Press

`Ctrl + Shift + ``or select*New Terminal*from the*Terminal*menu to open a new integrated terminal in VS Code.Compile your custom handler using the following command. An executable file named

`handler`

(`handler.exe`

on Windows) is output in the function app root folder.`go build handler.go`


## Configure your function app

The function host needs to be configured to run your custom handler binary when it starts.

Open

*host.json*.In the

`customHandler.description`

section, set the value of`defaultExecutablePath`

to`handler`

(on Windows, set it to`handler.exe`

).In the

`customHandler`

section, add a property named`enableForwardingHttpRequest`

and set its value to`true`

. For functions consisting of only an HTTP trigger, this setting simplifies programming by allow you to work with a typical HTTP request instead of the custom handler[request payload](functions-custom-handlers#request-payload).Confirm the

`customHandler`

section looks like this example. Save the file.`"customHandler": { "description": { "defaultExecutablePath": "handler", "workingDirectory": "", "arguments": [] }, "enableForwardingHttpRequest": true }`


The function app is configured to start your custom handler executable.

## Run the function locally

Verify your new function by running the project locally and calling the function endpoint.

Use this command to start the local Azure Functions runtime host in the root of the project folder:

`func start`

`npm install npm start`

`mvn clean package mvn azure-functions:run`

Toward the end of the output, the following lines appear:

... Now listening on: http://0.0.0.0:7071 Application started. Press Ctrl+C to shut down. Http Functions: HttpExample: [GET,POST] http://localhost:7071/api/HttpExample ...

Copy the URL of your

`HttpExample`

function from this output to a browser and browse to the function URL. You should receive a success response with a "hello world" message.Note

Because access key authorization isn't enforced when running locally, the function URL returned doesn't include the access key value and you don't need it to call your function.

When you're done, use

**Ctrl**+**C**and choose`y`

to stop the functions host.

## Create supporting Azure resources for your function

Before you can deploy your function code to Azure, you need to create these resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A default
[Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your functions. - A
[user-assigned managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview), which the Functions host uses to connect to the default storage account. - A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Use the Azure CLI commands in these steps to create the required resources.

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account. Skip this step when running in Azure Cloud Shell.`az login`

If you haven't already done so, use this

command to install the Application Insights extension:`az extension add`

`az extension add --name application-insights`

Use this

[az group create](/en-us/cli/azure/group#az-group-create)command to create a resource group named`AzureFunctionsQuickstart-rg`

in your chosen region:`az group create --name "AzureFunctionsQuickstart-rg" --location "<REGION>"`

In this example, replace

`<REGION>`

with a region near you that supports the Flex Consumption plan. Use the[az functionapp list-flexconsumption-locations](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-locations)command to view the list of currently supported regions.Use this

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)command to create a general-purpose storage account in your resource group and region:`az storage account create --name <STORAGE_NAME> --location "<REGION>" --resource-group "AzureFunctionsQuickstart-rg" \ --sku "Standard_LRS" --allow-blob-public-access false --allow-shared-key-access false`

In this example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Names must contain three to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account, which is[supported by Functions](storage-considerations#storage-account-requirements). This new account can only be accessed by using Microsoft Entra-authenticated identities that have been granted permissions to specific resources.Use this script to create a user-assigned managed identity, parse the returned JSON properties of the object using

`jq`

, and grant`Storage Blob Data Owner`

permissions in the default storage account:`output=$(az identity create --name "func-host-storage-user" --resource-group "AzureFunctionsQuickstart-rg" --location <REGION> \ --query "{userId:id, principalId: principalId, clientId: clientId}" -o json) userId=$(echo $output | jq -r '.userId') principalId=$(echo $output | jq -r '.principalId') clientId=$(echo $output | jq -r '.clientId') storageId=$(az storage account show --resource-group "AzureFunctionsQuickstart-rg" --name <STORAGE_NAME> --query 'id' -o tsv) az role assignment create --assignee-object-id $principalId --assignee-principal-type ServicePrincipal \ --role "Storage Blob Data Owner" --scope $storageId`

If you don't have the

`jq`

utility in your local Bash shell, it's available in Azure Cloud Shell. In this example, replace`<STORAGE_NAME>`

and`<REGION>`

with your default storage account name and region, respectively.The

[az identity create](/en-us/cli/azure/identity#az-identity-create)command creates an identity named`func-host-storage-user`

. The returned`principalId`

is used to assign permissions to this new identity in the default storage account by using thecommand. The`az role assignment create`

command is used to obtain the storage account ID.`az storage account show`

Use this

[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)command to create the function app in Azure:`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime dotnet-isolated --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime java --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime node --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime python --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime python --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime other --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

In this example, replace these placeholders with the appropriate values:

`<APP_NAME>`

: a globally unique name appropriate to you. The`<APP_NAME>`

is also the default DNS domain for the function app.`<STORAGE_NAME>`

: the name of the account you used in the previous step.`<REGION>`

: your current region.`<LANGUAGE_VERSION>`

: use the same[supported language stack version](supported-languages)you verified locally, when applicable.

This command creates a function app running in your specified language runtime on Linux in the

[Flex Consumption Plan](flex-consumption-plan), which is free for the amount of usage you incur here. The command also creates an associated Azure Application Insights instance in the same resource group, with which you can use to monitor your function app executions and view logs. For more information, see[Monitor Azure Functions](functions-monitoring). The instance incurs no costs until you activate it.Use this script to add your user-assigned managed identity to the

[Monitoring Metrics Publisher](../role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher)role in your Application Insights instance:`appInsights=$(az monitor app-insights component show --resource-group "AzureFunctionsQuickstart-rg" \ --app <APP_NAME> --query "id" --output tsv) principalId=$(az identity show --name "func-host-storage-user" --resource-group "AzureFunctionsQuickstart-rg" \ --query principalId -o tsv) az role assignment create --role "Monitoring Metrics Publisher" --assignee $principalId --scope $appInsights`

In this example, replace

`<APP_NAME>`

with the name of your function app. The[az role assignment create](/en-us/cli/azure/role/assignment#az-role-assignment-create)command adds your user to the role. The resource ID of your Application Insights instance and the principal ID of your user are obtained by using the[az monitor app-insights component show](/en-us/cli/azure/monitor/app-insights/component#az-monitor-app-insights-component-show)andcommands, respectively.`az identity show`


## Update application settings

To enable the Functions host to connect to the default storage account by using shared secrets, replace the `AzureWebJobsStorage`

connection string setting with several settings that are prefixed with `AzureWebJobsStorage__`

. These settings define a complex setting that your app uses to connect to storage and Application Insights with a user-assigned managed identity.

Use this script to get the client ID of the user-assigned managed identity and uses it to define managed identity connections to both storage and Application Insights:

`clientId=$(az identity show --name func-host-storage-user \ --resource-group AzureFunctionsQuickstart-rg --query 'clientId' -o tsv) az functionapp config appsettings set --name <APP_NAME> --resource-group "AzureFunctionsQuickstart-rg" \ --settings AzureWebJobsStorage__accountName=<STORAGE_NAME> \ AzureWebJobsStorage__credential=managedidentity AzureWebJobsStorage__clientId=$clientId \ APPLICATIONINSIGHTS_AUTHENTICATION_STRING="ClientId=$clientId;Authorization=AAD"`

In this script, replace

`<APP_NAME>`

and`<STORAGE_NAME>`

with the names of your function app and storage account, respectively.Run the

[az functionapp config appsettings delete](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-delete)command to remove the existing`AzureWebJobsStorage`

connection string setting, which contains a shared secret key:`az functionapp config appsettings delete --name <APP_NAME> --resource-group "AzureFunctionsQuickstart-rg" --setting-names AzureWebJobsStorage`

In this example, replace

`<APP_NAME>`

with the names of your function app.

At this point, the Functions host can connect to the storage account securely by using managed identities instead of shared secrets. You can now deploy your project code to the Azure resources.

## Deploy the function project to Azure

After you've successfully created your function app in Azure, you're now ready to deploy your local functions project by using the [ func azure functionapp publish](functions-run-local#project-file-deployment) command.

In your root project folder, run this

command:`func azure functionapp publish`

`func azure functionapp publish <APP_NAME>`

In this example, replace

`<APP_NAME>`

with the name of your app. A successful deployment shows results similar to the following output (truncated for simplicity):... Getting site publishing info... Creating archive for current directory... Performing remote build for functions project. ... Deployment successful. Remote build succeeded! Syncing triggers... Functions in msdocs-azurefunctions-qs: HttpExample - [httpTrigger] Invoke url: https://msdocs-azurefunctions-qs.azurewebsites.net/api/httpexample

In your local terminal or command prompt, run this command to get the URL endpoint value, including the access key:

`func azure functionapp list-functions <APP_NAME> --show-keys`

In this example, again replace

`<APP_NAME>`

with the name of your app.Copy the returned endpoint URL and key, which you use to invoke the function endpoint.


## Update the pom.xml file

After you successfully create your function app in Azure, update the pom.xml file so that Maven can deploy to your new app. Otherwise, Maven creates a new set of Azure resources during deployment.

In Azure Cloud Shell, use this

command to get the deployment container URL and ID of the new user-assigned managed identity:`az functionapp show`

`az functionapp show --name <APP_NAME> --resource-group AzureFunctionsQuickstart-rg \ --query "{userAssignedIdentityResourceId: properties.functionAppConfig.deployment.storage.authentication.userAssignedIdentityResourceId, \ containerUrl: properties.functionAppConfig.deployment.storage.value}"`

In this example, replace

`<APP_NAME>`

with the names of your function app.In the project root directory, open the pom.xml file in a text editor, locate the

`properties`

element, and update these specific property values:Property name Value `java.version`

Use the same [supported language stack version](supported-languages)you verified locally, such as`17`

.`azure.functions.maven.plugin.version`

`1.37.1`

`azure.functions.java.library.version`

`3.1.0`

`functionAppName`

The name of your function app in Azure. Find the

`configuration`

section of the`azure-functions-maven-plugin`

and replace it with this XML fragment:`<configuration> <appName>${functionAppName}</appName> <resourceGroup>AzureFunctionsQuickstart-rg</resourceGroup> <pricingTier>Flex Consumption</pricingTier> <region>....</region> <runtime> <os>linux</os> <javaVersion>${java.version}</javaVersion> </runtime> <deploymentStorageAccount>...</deploymentStorageAccount> <deploymentStorageResourceGroup>AzureFunctionsQuickstart-rg</deploymentStorageResourceGroup> <deploymentStorageContainer>...</deploymentStorageContainer> <storageAuthenticationMethod>UserAssignedIdentity</storageAuthenticationMethod> <userAssignedIdentityResourceId>...</userAssignedIdentityResourceId> <appSettings> <property> <name>FUNCTIONS_EXTENSION_VERSION</name> <value>~4</value> </property> </appSettings> </configuration>`

In the new

`configuration`

element, make these specific replacements of the ellipses (`...`

) values:Configuration Value `region`

The region code of your existing function app, such as `eastus`

.`deploymentStorageAccount`

The name of your storage account. `deploymentStorageContainer`

The name of the deployment share, which comes after the `\`

in the`containerUrl`

value you obtained.`userAssignedIdentityResourceId`

The fully qualified resource ID of your managed identity, which you obtained. Save your changes to the

*pom.xml*file.

You can now use Maven to deploy your code project to your existing app.

## Deploy the function project to Azure

From the command prompt, run this command:

`mvn clean package azure-functions:deploy`

After your deployment succeeds, run this Core Tools command to get the URL endpoint value, including the access key:

`func azure functionapp list-functions <APP_NAME> --show-keys`

In this example, again replace

`<APP_NAME>`

with the name of your app.Copy the returned endpoint URL and key, which you use to invoke the function endpoint.


## Invoke the function on Azure

Because your function uses an HTTP trigger and supports GET requests, you invoke it by making an HTTP request to its URL using the function-level access key. It's easiest to execute a GET request in a browser.

Paste the URL and access key you copied into a browser address bar.

The endpoint URL should look something like this example:

`https://contoso-app.azurewebsites.net/api/httpexample?code=aabbccdd...`


In this case, you must also provide an access key in the query string when making a GET request to the endpoint URL. Using an access key is recommended to limit access from random clients. When making a POST request using an HTTP client, you should instead provide the access key in the `x-functions-key`

header.

When you navigate to this URL, the browser should display similar output as when you ran the function locally.

## Clean up resources

If you continue to the [next step](#next-steps) and add an Azure Storage queue output binding, keep all your resources in place as you'll build on what you've already done.

Otherwise, use the following command to delete the resource group and all its contained resources to avoid incurring further costs.

```
az group delete --name AzureFunctionsQuickstart-rg
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/security-concepts -->

# Securing Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure App Service](../app-service/) provides the hosting infrastructure for your function apps. This article provides security strategies for running your function code, and how App Service can help you secure your functions.

Azure App Service actively secures and hardens its platform components, including Azure virtual machines (VMs), storage, network connections, web frameworks, and management and integration features. App Service undergoes continuous, rigorous compliance checks to ensure that:

[Each app is segregated from other Azure apps and resources](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox).[Regular updates of VMs and runtime software](/en-us/azure/app-service/overview-patch-os-runtime)address newly discovered vulnerabilities.- Communication of secrets and connection strings between apps and other Azure resources like
[Azure SQL Database](https://azure.microsoft.com/services/sql-database/)occurs only within Azure, without crossing any network boundaries. Stored secrets are always encrypted. - All communications over App Service connectivity features like
[Hybrid Connection](/en-us/azure/app-service/app-service-hybrid-connections)are encrypted. - All connections via remote management tools like Azure PowerShell, Azure CLI, Azure SDKs, and REST APIs are encrypted.
- Continuous threat management protects the infrastructure and platform against malware, distributed denial-of-service (DDoS) and man-in-the-middle attacks, and other threats.

For more information on infrastructure and platform security in Azure, see the [Azure Trust Center](https://www.microsoft.com/trust-center).

For a set of security recommendations that follow the [Microsoft cloud security benchmark](/en-us/security/benchmark/azure/introduction), see [Azure Security Baseline for Azure Functions](/en-us/security/benchmark/azure/baselines/functions-security-baseline).

While planning for secure development, deployment, and operation of serverless functions is much the same as for any web-based or cloud-hosted application, serverless applications are likely vulnerable to variations of traditional attacks. To learn more about potential attacks on serverless infrastructure, see the [OWASP Top 10: Serverless Interpretation](https://owasp.org/www-project-serverless-top-10/).

## Secure operation

This section guides you on configuring and running your function app as securely as possible.

### Defender for Cloud

Defender for Cloud integrates with your function app in the portal. It provides a quick assessment of potential configuration-related security vulnerabilities. Function apps running in a dedicated plan can also use Defender for Cloud's enhanced security features for an extra cost. For more information, see [Defender for App Service](/en-us/azure/defender-for-cloud/defender-for-app-service-introduction).

### Log and monitor

One way to detect attacks is through activity monitoring and logging analytics. Functions integrates with Application Insights to collect log, performance, and error data for your function app. Application Insights automatically detects performance anomalies and includes powerful analytics tools to help you diagnose issues and understand how your functions are used. For more information, see [Monitor Azure Functions](functions-monitoring).

Functions also integrates with Azure Monitor Logs to enable you to consolidate function app logs with system events for easier analysis. You can use diagnostic settings to configure the streaming export of platform logs and metrics for your functions to the destination of your choice, such as a Logs Analytics workspace. For more information, see [Monitoring Azure Functions with Azure Monitor Logs](functions-monitor-log-analytics).

For enterprise-level threat detection and response automation, stream your logs and events to a Logs Analytics workspace. You can then connect Microsoft Sentinel to this workspace. For more information, see [What is Microsoft Sentinel](../sentinel/overview).

For more security recommendations for observability, see the [Azure security baseline for Azure Functions](security-baseline#logging-and-monitoring).

### Secure HTTP endpoints

HTTP endpoints that you expose publicly provide a vector of attack for malicious actors. When securing your HTTP endpoints, use a layered security approach. Use these techniques to reduce the vulnerability of publicly exposed HTTP endpoints, ordered from most basic to most secure and restrictive:

[Require HTTPS](#require-https)[Require access keys](#function-access-keys)[Enable App Service Authentication/Authorization](#enable-app-service-authenticationauthorization)[Use Azure API Management (APIM) to authenticate requests](#use-azure-api-management-apim-to-authenticate-requests)[Deploy your function app to a virtual network](#deploy-your-function-app-to-a-virtual-network)[Deploy your function app in isolation](#deploy-your-function-app-in-isolation)

### Require HTTPS

By default, clients can connect to function endpoints by using either HTTP or HTTPS. Redirect HTTP to HTTPS because HTTPS uses the TLS protocol to provide a secure connection, which is both encrypted and authenticated. To learn how, see [Enforce HTTPS](../app-service/configure-ssl-bindings#enforce-https).

When you require HTTPS, also require the latest TLS version. To learn how, see [Enforce TLS versions](../app-service/configure-ssl-bindings#enforce-tls-versions).

For more information, see [Secure connections (TLS)](../app-service/overview-security#https-and-certificates).

### Function access keys

Functions uses keys to make it harder to access your function endpoints. Unless you set the HTTP access level on an HTTP triggered function to `anonymous`

, requests must include an access key in the request. For more information, see [Work with access keys in Azure Functions](function-keys-how-to).

While access keys can help prevent unwanted access, the only way to truly secure your function endpoints is by implementing positive authentication of clients accessing your functions. You can then make authorization decisions based on identity.

For the highest level of security, secure the entire application architecture inside a virtual network [using private endpoints](#deploy-your-function-app-to-a-virtual-network) or by [running in isolation](#deploy-your-function-app-in-isolation).

### Disable administrative endpoints

Function apps can serve administrative endpoints under the `/admin`

route. You can use these endpoints for operations such as obtaining host status information and performing test invocations. When exposed, requests against these endpoints must include the app's master key. You can also access administrative operations through the [Azure Resource Manager Microsoft.Web/sites API](/en-us/rest/api/appservice/web-apps), which offers Azure RBAC. To disable the

`/admin`

endpoints, set the `functionsRuntimeAdminIsolationEnabled`

site property in your app to `true`

. For more information, see the [functionsRuntimeAdminIsolationEnabled](functions-app-settings#functionsruntimeadminisolationenabled)property reference.

### Enable App Service Authentication/Authorization

The App Service platform lets you use Microsoft Entra ID and several non-Microsoft identity providers to authenticate clients. Use this strategy to implement custom authorization rules for your functions. You can work with user information from your function code. For more information, see [Authentication and authorization in Azure App Service](../app-service/overview-authentication-authorization) and [Working with client identities](functions-bindings-http-webhook-trigger#working-with-client-identities).

### Use Azure API Management (APIM) to authenticate requests

APIM provides various API security options for incoming requests. For more information, see [API Management authentication policies](../api-management/api-management-policies#authentication-and-authorization). By using APIM, you can configure your function app to accept requests only from the IP address of your APIM instance. For more information, see [IP address restrictions](ip-addresses#ip-address-restrictions).

### Permissions

As with any application or service, run your function app with the lowest possible permissions.

#### User management permissions

Functions supports built-in [Azure role-based access control (Azure RBAC)](../role-based-access-control/overview). Azure roles supported by Functions are [Contributor](../role-based-access-control/built-in-roles#contributor), [Owner](../role-based-access-control/built-in-roles#owner), and [Reader](../role-based-access-control/built-in-roles#reader).

Permissions take effect at the function app level. The Contributor role is required to perform most function app-level tasks. You also need the Contributor role along with the [Monitoring Reader permission](/en-us/azure/azure-monitor/roles-permissions-security#monitoring-reader) to view log data in Application Insights. Only the Owner role can delete a function app.

#### Organize functions by privilege

Connection strings and other credentials stored in application settings give all of the functions in the function app the same set of permissions in the associated resource. Consider minimizing the number of functions with access to specific credentials by moving functions that don't use those credentials to a separate function app. You can always use techniques such as [function chaining](/en-us/training/modules/chain-azure-functions-data-using-bindings/) to pass data between functions in different function apps.

#### Managed identities

A managed identity from Microsoft Entra ID allows your app to easily access other Microsoft Entra-protected resources, such as Azure Key Vault. The Azure platform manages the identity, so you don't need to provision or rotate any secrets. For more information about managed identities in Microsoft Entra ID, see [Managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview).

You can grant two types of identities to your application:

- A
*system-assigned identity*is tied to the app and is deleted if the app is deleted. An app can have only one system-assigned identity. - A
*user-assigned identity*is a standalone Azure resource that can be assigned to your app. An app can have multiple user-assigned identities. One user-assigned identity can be assigned to multiple Azure resources, such as two App Service apps.

Use managed identities instead of secrets for connections from some triggers and bindings. See [Identity-based connections](#identity-based-connections).

For more information, see [Use managed identities for App Service and Azure Functions](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json).

#### Restrict CORS access

[Cross-origin resource sharing (CORS)](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) is a way to allow web apps running in another domain to make requests to your HTTP trigger endpoints. App Service provides built-in support for handling the required CORS headers in HTTP requests. CORS rules are defined on a function app level.

It's tempting to use a wildcard that allows all sites to access your endpoint. This approach defeats the purpose of CORS, which is to help prevent cross-site scripting attacks. Instead, add a separate CORS entry for the domain of each web app that must access your endpoint.

### Managing secrets

To connect to the various services and resources needed to run your code, function apps need access to secrets, such as connection strings and service keys. This section describes how to store secrets required by your functions.

Never store secrets in your function code.

#### Application settings

By default, store connection strings and secrets used by your function app and bindings as application settings. This approach makes these credentials available to both your function code and the various bindings used by the function. Use the application setting (key) name to retrieve the actual value, which is the secret.

For example, every function app requires an associated storage account, which the runtime uses. By default, you store the connection to this storage account in an application setting named `AzureWebJobsStorage`

.

Azure encrypts app settings and connection strings. The app settings and connection strings are decrypted only before being injected into your app's process memory when the app starts. The encryption keys are rotated regularly. If you prefer to manage the secure storage of your secrets, make the app settings references to Azure Key Vault secrets.

When developing functions on your local computer, you can also encrypt settings by default in the `local.settings.json`

file. For more information, see [Encrypt the local settings file](functions-run-local#encrypt-the-local-settings-file).

#### Key Vault references

While application settings are sufficient for most functions, you might want to share the same secrets across multiple services. In this case, redundant storage of secrets results in more potential vulnerabilities. A more secure approach is to use a central secret storage service and use references to this service instead of the secrets themselves.

[Azure Key Vault](/en-us/azure/key-vault/general/overview) is a service that provides centralized secrets management, with full control over access policies and audit history. You can use a Key Vault reference in the place of a connection string or key in your application settings. For more information, see [Use Key Vault references for App Service and Azure Functions](../app-service/app-service-key-vault-references?toc=/azure/azure-functions/toc.json).

### Identity-based connections

Use identities in place of secrets for connecting to some resources. This approach has the advantage of not requiring the management of a secret, and it provides more fine-grained access control and auditing.

When you write code that creates the connection to [Azure services that support Microsoft Entra authentication](../active-directory/managed-identities-azure-resources/services-support-managed-identities#services-supporting-managed-identities), you can use an identity instead of a secret or connection string. Details for both connection methods are covered in the documentation for each service.

You can configure some Azure Functions binding extensions to access services by using identity-based connections. For more information, see [Configure an identity-based connection](functions-reference#configure-an-identity-based-connection).

### Set usage quotas

Consider setting a usage quota for functions running in a Consumption plan. When you set a daily GB-sec limit on the total execution of functions in your function app, execution stops when the limit is reached. This approach could potentially help protect against malicious code executing your functions. To learn how to estimate consumption for your functions, see [Estimating Consumption plan costs](functions-consumption-costs).

### Data validation

The triggers and bindings used by your functions don't provide any extra data validation. Your code must validate any data received from a trigger or input binding. If an upstream service is compromised, you don't want unvalidated inputs flowing through your functions. For example, if your function stores data from an Azure Storage queue in a relational database, you must validate the data and parameterize your commands to avoid SQL injection attacks.

Don't assume that the data coming into your function is already validated or sanitized. It's also a good idea to verify that the data being written to output bindings is valid.

### Handle errors

While it seems basic, it's important to write good error handling in your functions. Unhandled errors bubble up to the host, and the runtime handles these errors. Different bindings handle the processing of errors differently. For more information, see [Azure Functions error handling](functions-bindings-error-pages).

### Disable remote debugging

Make sure that remote debugging is disabled, except when you're actively debugging your functions. You can disable remote debugging in the **General Settings** tab of your function app **Configuration** in the portal.

### Restrict CORS access

Azure Functions supports cross-origin resource sharing (CORS). CORS is configured [in the portal](functions-how-to-use-azure-function-app-settings#cors) and through the [Azure CLI](/en-us/cli/azure/functionapp/cors). The CORS allowed origins list applies at the function app level. With CORS enabled, responses include the `Access-Control-Allow-Origin`

header. For more information, see [Cross-origin resource sharing](functions-how-to-use-azure-function-app-settings#cors).

Don't use wildcards in your allowed origins list. Instead, list the specific domains from which you expect to get requests.

### Store data encrypted

Azure Storage encrypts all data in a storage account at rest. For more information, see [Azure Storage encryption for data at rest](../storage/common/storage-service-encryption).

By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption of blob and file data. These keys must be present in Azure Key Vault for Functions to be able to access the storage account. To learn more, see [Encrypt your application data at rest using customer-managed keys](configure-encrypt-at-rest-using-cmk).

### Secure related resources

A function app frequently depends on other resources, so part of securing the app is securing these external resources. At a minimum, most function apps include a dependency on Application Insights and Azure Storage. For guidance on securing these resources, consult the [Azure security baseline for Azure Monitor](/en-us/security/benchmark/azure/baselines/azure-monitor-security-baseline) and the [Azure security baseline for Storage](/en-us/security/benchmark/azure/baselines/storage-security-baseline).

Important

The storage account is used to store important app data, sometimes including the application code itself. You should limit access from other apps and users to the storage account.

You should also consult the guidance for any resource types your application logic depends on, both as triggers and bindings and from your function code.

## Secure deployment

Azure Functions tooling integration makes it easy to publish local function project code to Azure. It's important to understand how deployment works when considering security for an Azure Functions topology.

### Deployment credentials

App Service deployments require a set of deployment credentials. You use these deployment credentials to secure your function app deployments. The App Service platform manages deployment credentials and encrypts them at rest.

There are two kinds of deployment credentials:

**User-scope**or user-level credentials provide one set of deployment credentials for a user's entire Azure account. A user who is granted app access via role-based access control (RBAC) or coadministrator permissions can use their user-level credentials as long as they have those permissions.You can use your user-scope credentials to deploy any app to App Service via local Git or FTP/S in any subscription that your Azure account has permission to access. You don't share these credentials with any other Azure users. You can reset your user-scope credentials anytime.

**App-scope**or application-level credentials are one set of credentials per app that can be used to deploy that app only. These credentials are generated automatically for each app at creation and can't be configured manually, but the password can be reset anytime.A user must have at least

**Contributor**level permissions on an app, including the built-in**Website Contributor**role, to be granted access to app-level credentials via RBAC.**Reader**role can't publish and can't access these credentials.

At this time, Key Vault isn't supported for deployment credentials. To learn more about managing deployment credentials, see [Configure deployment credentials for Azure App Service](../app-service/deploy-configure-credentials).

### Disable FTP

By default, each function app has an FTP endpoint enabled. The FTP endpoint is accessed using deployment credentials.

FTP isn't recommended for deploying your function code. FTP deployments are manual, and they require you to synchronize triggers. For more information, see [FTP deployment](functions-deployment-technologies#ftps).

When you're not using FTP, keep it disabled. You can change this setting in the portal. If you do choose to use FTP, [enforce FTPS](../app-service/deploy-ftp#enforce-ftps).

### Secure the `scm`

endpoint

Each function app has a corresponding `scm`

service endpoint that the Advanced Tools (Kudu) service uses for deployments and other App Service [site extensions](https://github.com/projectkudu/kudu/wiki/Azure-Site-Extensions). The `scm`

endpoint for a function app is always a URL in the form `https://<FUNCTION_APP_NAME>.scm.azurewebsites.net`

. When you use network isolation to secure your functions, you must also account for this endpoint.

By using a separate `scm`

endpoint, you can control deployments and other Advanced Tools functionalities for function apps that are isolated or running in a virtual network. The `scm`

endpoint supports both basic authentication (by using deployment credentials) and single sign-on with your Azure portal credentials. For more information, see [Accessing the Kudu service](https://github.com/projectkudu/kudu/wiki/Accessing-the-kudu-service).

### Continuous security validation

Because you need to consider security at every step in the development process, it makes sense to also implement security validations in a continuous deployment environment. This approach is sometimes called *DevSecOps*. By using Azure DevOps for your deployment pipeline, you can integrate validation into the deployment process. For more information, see [Secure your Azure Pipelines](/en-us/azure/devops/pipelines/security/overview).

## Network security

By restricting network access to your function app, you can control who can access your functions endpoints. Functions uses App Service infrastructure to enable your functions to access resources without using internet-routable addresses or to restrict internet access to a function endpoint. To learn more about these networking options, see [Azure Functions networking options](functions-networking-options).

### Set access restrictions

Access restrictions allow you to define lists of allow and deny rules to control traffic to your app. Rules are evaluated in priority order. If you don't define any rules, your app accepts traffic from any address. For more information, see [Azure App Service access restrictions](../app-service/app-service-ip-restrictions?toc=/azure/azure-functions/toc.json).

### Secure the storage account

When you create a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. You can replace this storage account with one that is secured by a virtual network with access enabled by service endpoints or private endpoints. For more information, see [Restrict your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

### Deploy your function app to a virtual network

[Azure Private Endpoint](../private-link/private-endpoint-overview) is a network interface that connects you privately and securely to a service powered by Azure Private Link. Private Endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network.

You can use Private Endpoint for your functions hosted in the [Flex Consumption](flex-consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) plans.

If you want to make calls to Private Endpoints, then you must make sure that your DNS lookups resolve to the private endpoint. You can enforce this behavior in one of the following ways:

- Integrate with Azure DNS private zones. When your virtual network doesn't have a custom DNS server, this is done automatically.
- Manage the private endpoint in the DNS server used by your app. To manage a private endpoint, you must know the endpoint address and use an A record to reference the endpoint you're trying to reach.
- Configure your own DNS server to forward to
[Azure DNS private zones](../dns/private-dns-privatednszone).

To learn more, see [using Private Endpoints for Web Apps](../app-service/networking/private-endpoint).

### Deploy your function app in isolation

Azure App Service Environment provides a dedicated hosting environment in which to run your functions. These environments let you configure a single front-end gateway that you can use to authenticate all incoming requests. For more information, see [Integrate your ILB App Service Environment with the Azure Application Gateway](../app-service/environment/integrate-with-application-gateway).

### Use a gateway service

By using gateway services such as [Azure Application Gateway](../application-gateway/overview) and [Azure Front Door](../frontdoor/front-door-overview), you can set up a Web Application Firewall (WAF). WAF rules monitor or block detected attacks, which provides an extra layer of protection for your functions. To set up a WAF, your function app needs to run in an ASE or use Private Endpoints (preview). For more information, see [Using private endpoints](../app-service/networking/private-endpoint).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitoring -->

# Monitor executions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Functions](functions-overview) offers built-in integration with Azure Application Insights to monitor functions executions. This article provides an overview of the monitoring capabilities provided by Azure for monitoring Azure Functions.

Application Insights collects log, performance, and error data. By automatically detecting performance anomalies and featuring powerful analytics tools, you can more easily diagnose issues and better understand how your functions are used. These tools are designed to help you continuously improve performance and usability of your functions. You can even use Application Insights during local function app project development. For more information, see [Introduction to Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview).

As Application Insights instrumentation is built into Azure Functions, you need a valid instrumentation key to connect your function app to an Application Insights resource. The instrumentation key is added to your application settings as you create your function app resource in Azure. If your function app doesn't already have this key, you can [set it manually](configure-monitoring#enable-application-insights-integration).

You can also monitor the function app itself by using Azure Monitor. To learn more, see [Monitor Azure Functions](monitor-functions).

## Application Insights pricing and limits

You can try out Application Insights integration with Azure Functions for free featuring a daily limit to how much data is processed for free.

If you enable Applications Insights during development, you might hit this limit during testing. Azure provides portal and email notifications when you're approaching your daily limit. If you miss those alerts and hit the limit, new logs don't appear in Application Insights queries. Be aware of the limit to avoid unnecessary troubleshooting time. For more information, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing).

Important

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. Sampling is enabled by default. If you appear to be missing data, you might need to adjust the sampling settings to fit your particular monitoring scenario. To learn more, see [Configure sampling](configure-monitoring#configure-sampling).

## Application Insights integration

Typically, you create an Application Insights instance when you create your function app. In this case, the instrumentation key required for the integration is already set as an application setting named `APPINSIGHTS_INSTRUMENTATIONKEY`

. If for some reason your function app doesn't have the instrumentation key set, you need to [enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

Important

Sovereign clouds, such as Azure Government, require the use of the Application Insights connection string (`APPLICATIONINSIGHTS_CONNECTION_STRING`

) instead of the instrumentation key. To learn more, see the [APPLICATIONINSIGHTS_CONNECTION_STRING reference](functions-app-settings#applicationinsights_connection_string).

The following table details the supported features of Application Insights available for monitoring your function apps:

| Azure Functions runtime version | 1.x | 4.x+ |
|---|---|---|
Automatic collection of |
||
| • Requests | ✓ | ✓ |
| • Exceptions | ✓ | ✓ |
| • Performance Counters | ✓ | ✓ |
| • Dependencies | ||
| — HTTP | ✓ | |
| — Service Bus | ✓ | |
| — Event Hubs | ✓ | |
| — SQL* | ✓ | |
Supported features |
||
| • QuickPulse/LiveMetrics | Yes | Yes |
| — Secure Control Channel | Yes | |
| • Sampling | Yes | Yes |
| • Heartbeats | Yes | |
Correlation |
||
| • Service Bus | Yes | |
| • Event Hubs | Yes | |
Configurable |
||
| •
|

* To enable the collection of SQL query string text, see [Enable SQL query collection](configure-monitoring#enable-sql-query-collection).

## Collecting telemetry data

With Application Insights integration enabled, telemetry data is sent to your connected Application Insights instance. This data includes logs generated by the Functions host, traces written from your functions code, and performance data.

Note

In addition to data from your functions and the Functions host, you can also collect data from the [Functions scale controller](#scale-controller-logs).

### Log levels and categories

When you write traces from your application code, you should assign a log level to the traces. Log levels provide a way for you to limit the amount of data that is collected from your traces.

A *log level* is assigned to every log. The value is an integer that indicates relative importance:

| LogLevel | Code | Description |
|---|---|---|
| Trace | 0 | Logs that contain the most detailed messages. These messages might contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |
| Debug | 1 | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Information | 2 | Logs that track the general flow of the application. These logs should have long-term value. |
| Warning | 3 | Logs that highlight an abnormal or unexpected event in the application flow, but don't otherwise cause the application execution to stop. |
| Error | 4 | Logs that highlight when the current flow of execution is stopped because of a failure. These errors should indicate a failure in the current activity, not an application-wide failure. |
| Critical | 5 | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| None | 6 | Disables logging for the specified category. |

The [ host.json file](functions-host-json) configuration determines how much logging a functions app sends to Application Insights.

To learn more about log levels, see [Configure log levels](configure-monitoring#configure-log-levels).

By assigning logged items to a category, you have more control over telemetry generated from specific sources in your function app. Categories make it easier to run analytics over collected data. Traces written from your function code are assigned to individual categories based on the function name. To learn more about categories, see [Configure categories](configure-monitoring#configure-categories).

### Custom telemetry data

In [C#](functions-dotnet-class-library#log-custom-telemetry-in-c-functions), [JavaScript](functions-reference-node#track-custom-data), and [Python](functions-reference-python#logging-and-monitoring), you can use an Application Insights SDK to write custom telemetry data.

### Dependencies

Starting with version 2.x of Functions, Application Insights automatically collects data on dependencies for bindings that use certain client SDKs. Application Insights collects data on the following dependencies:

- Azure Cosmos DB
- Azure Event Hubs
- Azure Service Bus
- Azure Storage services (Blob, Queue, and Table)

HTTP requests and database calls using `SqlClient`

are also captured. For the complete list of dependencies supported by Application Insights, see [automatically tracked dependencies](/en-us/azure/azure-monitor/app/asp-net-dependencies#automatically-tracked-dependencies).

Application Insights generates an *application map* of collected dependency data. The following is an example of an application map of an HTTP trigger function with a Queue storage output binding.


Dependencies are written at the `Information`

level. If you filter at `Warning`

or above, you don't see the dependency data. Also, automatic collection of dependencies happens at a non-user scope. To capture dependency data, make sure the level is set to at least `Information`

outside the user scope (`Function.<YOUR_FUNCTION_NAME>.User`

) in your host.

In addition to automatic dependency data collection, you can also use one of the language-specific Application Insights SDKs to write custom dependency information to the logs. For an example how to write custom dependencies, see one of the following language-specific examples:

[Log custom telemetry in C# functions](functions-dotnet-class-library#log-custom-telemetry-in-c-functions)[Log custom telemetry in JavaScript functions](functions-reference-node#track-custom-data)[Log custom telemetry in Python functions](functions-reference-python#logging-and-monitoring)

### Performance Counters

Automatic collection of Performance Counters isn't supported when running on Linux.

## Writing to logs

The way that you write to logs and the APIs you use depend on the language of your function app project. See the developer guide for your language to learn more about writing logs from your functions.

## Analyze data

By default, the data collected from your function app is stored in Application Insights. In the [Azure portal](https://portal.azure.com), Application Insights provides an extensive set of visualizations of your telemetry data. You can drill into error logs and query events and metrics. To learn more, including basic examples of how to view and query your collected data, see [Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data).

## Streaming Logs

While developing an application, you often want to see what's being written to the logs in near real time when running in Azure.

There are two ways to view a stream of the log data being generated by your function executions.

**Built-in log streaming**: the App Service platform lets you view a stream of your application log files. This stream is equivalent to the output seen when you debug your functions during[local development](functions-develop-local)and when you use the**Test**tab in the portal. All log-based information is displayed. For more information, see[Stream logs](../app-service/troubleshoot-diagnostic-logs#stream-logs). This streaming method supports only a single instance, and can't be used with an app running on Linux in a Consumption plan.**Live Metrics Stream**: when your function app is[connected to Application Insights](configure-monitoring#enable-application-insights-integration), you can view log data and other metrics in near real time in the Azure portal using[Live Metrics Stream](/en-us/azure/azure-monitor/app/live-stream). Use this method when monitoring functions running on multiple-instances or on Linux in a Consumption plan. This method uses[sampled data](configure-monitoring#configure-sampling).

Log streams can be viewed both in the portal and in most local development environments. To learn how to enable log streams, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## Diagnostic logs

Application Insights lets you export telemetry data to long-term storage or other analysis services.

Because Functions also integrates with Azure Monitor, you can also use diagnostic settings to send telemetry data to various destinations, including Azure Monitor logs. To learn more, see [Monitor Azure Functions](functions-monitor-log-analytics).

## Scale controller logs

The [Azure Functions scale controller](event-driven-scaling#runtime-scaling) monitors instances of the Azure Functions host on which your app runs. This controller makes decisions about when to add or remove instances based on current performance. You can have the scale controller emit logs to Application Insights to better understand the decisions the scale controller is making for your function app. You can also store the generated logs in Blob storage for analysis by another service.

To enable this feature, you add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. To learn how, see [Configure scale controller logs](configure-monitoring#configure-scale-controller-logs).

## Azure Monitor metrics

In addition to log-based telemetry data collected by Application Insights, you can also get data about how the function app is running from [Azure Monitor Metrics](/en-us/azure/azure-monitor/essentials/data-platform-metrics). To learn more, see [Monitor Azure Functions](monitor-functions).

## Report issues

To report an issue with Application Insights integration in Functions, or to make a suggestion or request, [create an issue in GitHub](https://github.com/Azure/Azure-Functions/issues/new).

## Next steps

For more information, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-terraform -->

# Quickstart: Create and deploy Azure Functions resources from Terraform

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use Terraform to create a function app in a Flex Consumption plan in Azure Functions, along with other required Azure resources. The Flex Consumption plan provides serverless hosting that lets you run your code on demand without explicitly provisioning or managing infrastructure. The function app runs on Linux and is configured to use Azure Blob storage for code deployments.

[Terraform](https://www.terraform.io) enables the definition, preview, and deployment of cloud infrastructure. Using Terraform, you create configuration files using [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration). The HCL syntax allows you to specify the cloud provider - such as Azure - and the elements that make up your cloud infrastructure. After you create your configuration files, you create an *execution plan* that allows you to preview your infrastructure changes before they're deployed. Once you verify the changes, you apply the execution plan to deploy the infrastructure.

- Create an Azure resource group with a unique name.
- Generate a random string of 13 lowercase letters to name resources.
- Create a storage account in Azure.
- Create a blob storage container in the storage account.
- Create a Flex Consumption plan in Azure Functions.
- Create a function app with a Flex Consumption plan in Azure.
- Output the names of the resource group, storage account, service plan, function app, and Azure Functions Flex Consumption plan.

## Prerequisites

- Create an Azure account with an active subscription. You can
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). [Install and configure Terraform](/en-us/azure/developer/terraform/quickstart-configure).[Install the Azure CLI](/en-us/cli/azure/install-azure-cli)to obtain the subscription ID or run in[Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

## Implement the Terraform code

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-functions). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-functions/TestRecord.md). See more [articles and sample code showing how to use Terraform to manage Azure resources](/en-us/azure/terraform).

Create a directory in which to test and run the sample Terraform code, and make it the current directory.

Create a file named

`main.tf`

, and insert the following code:`# This Terraform configuration creates a Flex Consumption plan app in Azure Functions # with the required Storage account and Blob Storage deployment container. # Create a random pet to generate a unique resource group name resource "random_pet" "rg_name" { prefix = var.resource_group_name_prefix } # Create a resource group resource "azurerm_resource_group" "example" { location = var.resource_group_location name = random_pet.rg_name.id } # Random String for unique naming of resources resource "random_string" "name" { length = 8 special = false upper = false lower = true numeric = false } # Create a storage account resource "azurerm_storage_account" "example" { name = coalesce(var.sa_name, random_string.name.result) resource_group_name = azurerm_resource_group.example.name location = azurerm_resource_group.example.location account_tier = var.sa_account_tier account_replication_type = var.sa_account_replication_type } # Create a storage container resource "azurerm_storage_container" "example" { name = "example-flexcontainer" storage_account_id = azurerm_storage_account.example.id container_access_type = "private" } # Create a Log Analytics workspace for Application Insights resource "azurerm_log_analytics_workspace" "example" { name = coalesce(var.ws_name, random_string.name.result) location = azurerm_resource_group.example.location resource_group_name = azurerm_resource_group.example.name sku = "PerGB2018" retention_in_days = 30 } # Create an Application Insights instance for monitoring resource "azurerm_application_insights" "example" { name = coalesce(var.ai_name, random_string.name.result) location = azurerm_resource_group.example.location resource_group_name = azurerm_resource_group.example.name application_type = "web" workspace_id = azurerm_log_analytics_workspace.example.id } # Create a service plan resource "azurerm_service_plan" "example" { name = coalesce(var.asp_name, random_string.name.result) resource_group_name = azurerm_resource_group.example.name location = azurerm_resource_group.example.location sku_name = "FC1" os_type = "Linux" } # Create a function app resource "azurerm_function_app_flex_consumption" "example" { name = coalesce(var.fa_name, random_string.name.result) resource_group_name = azurerm_resource_group.example.name location = azurerm_resource_group.example.location service_plan_id = azurerm_service_plan.example.id storage_container_type = "blobContainer" storage_container_endpoint = "${azurerm_storage_account.example.primary_blob_endpoint}${azurerm_storage_container.example.name}" storage_authentication_type = "StorageAccountConnectionString" storage_access_key = azurerm_storage_account.example.primary_access_key runtime_name = var.runtime_name runtime_version = var.runtime_version maximum_instance_count = 50 instance_memory_in_mb = 2048 site_config { } }`

Create a file named

`outputs.tf`

, and insert the following code:`output "resource_group_name" { value = azurerm_resource_group.example.name } output "sa_name" { value = azurerm_storage_account.example.name } output "asp_name" { value = azurerm_service_plan.example.name } output "fa_name" { value = azurerm_function_app_flex_consumption.example.name } output "fa_url" { value = "https://${azurerm_function_app_flex_consumption.example.name}.azurewebsites.net" }`

Create a file named

`providers.tf`

, and insert the following code:`terraform { required_version = ">=1.0" required_providers { azurerm = { source = "hashicorp/azurerm" version = "~>4.0" } random = { source = "hashicorp/random" version = "~>3.0" } } } provider "azurerm" { features {} }`

Create a file named

`variables.tf`

, and insert the following code:`variable "resource_group_name" { type = string default = "" description = "The name of the Azure resource group. If blank, a random name will be generated." } variable "resource_group_name_prefix" { type = string default = "rg" description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription." } variable "resource_group_location" { type = string default = "eastus" description = "Location of the resource group." } variable "sa_account_tier" { description = "The tier of the storage account. Possible values are Standard and Premium." type = string default = "Standard" } variable "sa_account_replication_type" { description = "The replication type of the storage account. Possible values are LRS, GRS, RAGRS, and ZRS." type = string default = "LRS" } variable "sa_name" { description = "The name of the storage account. If blank, a random name will be generated." type = string default = "" } variable "ws_name" { description = "The name of the Log Analytics workspace. If blank, a random name will be generated." type = string default = "" } variable "ai_name" { description = "The name of the Application Insights instance. If blank, a random name will be generated." type = string default = "" } variable "asp_name" { description = "The name of the App Service Plan. If blank, a random name will be generated." type = string default = "" } variable "fa_name" { description = "The name of the Function App. If blank, a random name will be generated." type = string default = "" } variable "runtime_name" { description = "The name of the language worker runtime." type = string default = "node" # Allowed: dotnet-isolated, java, node, powershell, python } variable "runtime_version" { description = "The version of the language worker runtime." type = string default = "20" # Supported versions: see https://aka.ms/flexfxversions }`

Use this Azure CLI command to set the

`ARM_SUBSCRIPTION_ID`

environment variable to the ID of your current subscription:`export ARM_SUBSCRIPTION_ID=$(az account show --query "id" --output tsv)`

You must have this variable set for Terraform to be able to authenticate to your Azure subscription.


## Initialize Terraform

Run [terraform init](https://www.terraform.io/docs/commands/init.html) to initialize the Terraform deployment. This command downloads the Azure provider required to manage your Azure resources.

```
terraform init -upgrade
```


**Key points:**

- The
`-upgrade`

parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## Create a Terraform execution plan

Run [terraform plan](https://www.terraform.io/docs/commands/plan.html) to create an execution plan.

```
terraform plan -out main.tfplan -var="runtime_name=dotnet-isolated" -var="runtime_version=8"
```


```
terraform plan -out main.tfplan -var="runtime_name=powershell" -var="runtime_version=7.4"
```


```
terraform plan -out main.tfplan -var="runtime_name=python" -var="runtime_version=3.12"
```


```
terraform plan -out main.tfplan -var="runtime_name=java" -var="runtime_version=21"
```


```
terraform plan -out main.tfplan -var="runtime_name=node" -var="runtime_version=20"
```


Make sure that `runtime_version`

matches the language stack version you verified locally. Select your preferred language stack at the [top](#top) of the article.

**Key points:**

- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

## Apply a Terraform execution plan

Run [terraform apply](https://www.terraform.io/docs/commands/apply.html) to apply the execution plan to your cloud infrastructure.

```
terraform apply main.tfplan
```


**Key points:**

- The example
`terraform apply`

command assumes you previously ran`terraform plan -out main.tfplan`

. - If you specified a different filename for the
`-out`

parameter, use that same filename in the call to`terraform apply`

. - If you didn't use the
`-out`

parameter, call`terraform apply`

without any parameters.

## Verify the results

The `outputs.tf`

file returns these values for your new function app:

| Value | Description |
|---|---|
`resource_group_name` |
The name of the resource group you created. |
`sa_name` |
The name of the Azure storage account required by the Functions host. |
`asp_name` |
The name of the Flex Consumption plan that hosts your new app. |
`fa_name` |
The name of your new function app. |
`fa_url` |
The URL of your new function app endpoint. |

Open a browser and browse to the URL location in `fa_url`

. You can also use the [terraform output](https://developer.hashicorp.com/terraform/cli/commands/output) command to review these values at a later time.


## Clean up resources

When you no longer need the resources created via Terraform, do the following steps:

Run

[terraform plan](https://www.terraform.io/docs/commands/plan.html)and specify the`destroy`

flag.`terraform plan -destroy -out main.destroy.tfplan`

**Key points:**- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

- The
Run

[terraform apply](https://www.terraform.io/docs/commands/apply.html)to apply the execution plan.`terraform apply main.destroy.tfplan`


## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/en-us/azure/developer/terraform/troubleshoot).

## Next steps

You can now deploy a code project to the function app resources you created in Azure.

You can create, verify, and deploy a code project to your new function app from these local environments:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-output -->

# Azure SQL output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure SQL output binding lets you write to a database.

For information on setup and configuration details, see the [overview](functions-bindings-azure-sql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


To return [multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings) in our samples, we create a custom return type:

```
public static class OutputType
{
[SqlOutput("dbo.ToDo", connectionStringSetting: "SqlConnectionString")]
public static ToDoItem ToDoItem { get; set; }
public static HttpResponseData HttpResponse { get; set; }
}
```


### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database, using data provided in an HTTP POST request as a JSON body. The return object is the `OutputType`

class we created to handle both an HTTP response and the SQL output binding.

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace AzureSQL.ToDo
{
public static class PostToDo
{
// create a new ToDoItem from body object
// uses output binding to insert new item into ToDo table
[FunctionName("PostToDo")]
public static async Task<OutputType> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "PostFunction")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("PostToDo");
logger.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
ToDoItem toDoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
// generate a new id for the todo item
toDoItem.Id = Guid.NewGuid();
// set Url from env variable ToDoUri
toDoItem.url = Environment.GetEnvironmentVariable("ToDoUri")+"?id="+toDoItem.Id.ToString();
// if completed is not provided, default to false
if (toDoItem.completed == null)
{
toDoItem.completed = false;
}
return new OutputType()
{
ToDoItem = toDoItem,
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.Created)
}
}
}
public static class OutputType
{
[SqlOutput("dbo.ToDo", connectionStringSetting: "SqlConnectionString")]
public ToDoItem ToDoItem { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
}
```


### HTTP trigger, write to two tables

The following example shows a [C# function](functions-dotnet-class-library) that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


To use an extra output binding, we add a class for `RequestLog`

and modify our `OutputType`

class:

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace AzureSQL.ToDo
{
public static class PostToDo
{
// create a new ToDoItem from body object
// uses output binding to insert new item into ToDo table
[FunctionName("PostToDo")]
public static async Task<OutputType> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "PostFunction")] HttpRequestData req,
FunctionContext executionContext)
{
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
ToDoItem toDoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
// generate a new id for the todo item
toDoItem.Id = Guid.NewGuid();
// set Url from env variable ToDoUri
toDoItem.url = Environment.GetEnvironmentVariable("ToDoUri")+"?id="+toDoItem.Id.ToString();
// if completed is not provided, default to false
if (toDoItem.completed == null)
{
toDoItem.completed = false;
}
requestLog = new RequestLog();
requestLog.RequestTimeStamp = DateTime.Now;
requestLog.ItemCount = 1;
return new OutputType()
{
ToDoItem = toDoItem,
RequestLog = requestLog,
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.Created)
}
}
}
public class RequestLog {
public DateTime RequestTimeStamp { get; set; }
public int ItemCount { get; set; }
}
public static class OutputType
{
[SqlOutput("dbo.ToDo", connectionStringSetting: "SqlConnectionString")]
public ToDoItem ToDoItem { get; set; }
[SqlOutput("dbo.RequestLog", connectionStringSetting: "SqlConnectionString")]
public RequestLog RequestLog { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
}
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `ToDoItem`

class (in a separate file `ToDoItem.java`

) and a corresponding database table:

```
package com.function;
import java.util.UUID;
public class ToDoItem {
public UUID Id;
public int order;
public String title;
public String url;
public boolean completed;
public ToDoItem() {
}
public ToDoItem(UUID Id, int order, String title, String url, boolean completed) {
this.Id = Id;
this.order = order;
this.title = title;
this.url = url;
this.completed = completed;
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write a record to a table

The following example shows a SQL output binding in a Java function that adds a record to a table, using data provided in an HTTP POST request as a JSON body. The function takes another dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.sql.annotation.SQLOutput;
import com.google.gson.Gson;
import java.util.Optional;
public class PostToDo {
@FunctionName("PostToDo")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@SQLOutput(
name = "toDoItem",
commandText = "dbo.ToDo",
connectionStringSetting = "SqlConnectionString")
OutputBinding<ToDoItem> output) {
String json = request.getBody().get();
Gson gson = new Gson();
ToDoItem newToDo = gson.fromJson(json, ToDoItem.class);
newToDo.Id = UUID.randomUUID();
output.setValue(newToDo);
return request.createResponseBuilder(HttpStatus.CREATED).header("Content-Type", "application/json").body(output).build();
}
}
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding in a JavaS function that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings. The function takes another dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id INT IDENTITY(1,1) PRIMARY KEY,
RequestTimeStamp DATETIME2 NOT NULL DEFAULT(GETDATE()),
ItemCount INT NOT NULL
)
```


and Java class in `RequestLog.java`

:

```
package com.function;
import java.util.Date;
public class RequestLog {
public int Id;
public Date RequestTimeStamp;
public int ItemCount;
public RequestLog() {
}
public RequestLog(int Id, Date RequestTimeStamp, int ItemCount) {
this.Id = Id;
this.RequestTimeStamp = RequestTimeStamp;
this.ItemCount = ItemCount;
}
}
```


```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.sql.annotation.SQLOutput;
import com.google.gson.Gson;
import java.util.Optional;
public class PostToDoWithLog {
@FunctionName("PostToDoWithLog")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@SQLOutput(
name = "toDoItem",
commandText = "dbo.ToDo",
connectionStringSetting = "SqlConnectionString")
OutputBinding<ToDoItem> output,
@SQLOutput(
name = "requestLog",
commandText = "dbo.RequestLog",
connectionStringSetting = "SqlConnectionString")
OutputBinding<RequestLog> outputLog,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String json = request.getBody().get();
Gson gson = new Gson();
ToDoItem newToDo = gson.fromJson(json, ToDoItem.class);
newToDo.Id = UUID.randomUUID();
output.setValue(newToDo);
RequestLog newLog = new RequestLog();
newLog.ItemCount = 1;
outputLog.setValue(newLog);
return request.createResponseBuilder(HttpStatus.CREATED).header("Content-Type", "application/json").body(output).build();
}
}
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

This section contains the following examples:

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write records to a table

The following example shows a SQL output binding that adds records to a table, using data provided in an HTTP POST request as a JSON body.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const sqlOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL output binding function processed a request.');
const body = await request.json();
context.extraOutputs.set(sqlOutput, body);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const sqlOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlOutput],
handler: async (request, context) => {
context.log('HTTP trigger and SQL output binding function processed a request.');
const body = await request.json();
context.extraOutputs.set(sqlOutput, body);
return { status: 201 };
},
});
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const sqlTodoOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
const sqlRequestLogOutput = output.sql({
commandText: 'dbo.RequestLog',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL output binding function processed a request.');
const newLog = {
RequestTimeStamp: Date.now(),
ItemCount: 1,
};
context.extraOutputs.set(sqlRequestLogOutput, newLog);
const body = await request.json();
context.extraOutputs.set(sqlTodoOutput, body);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlTodoOutput, sqlRequestLogOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const sqlTodoOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
const sqlRequestLogOutput = output.sql({
commandText: 'dbo.RequestLog',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlTodoOutput, sqlRequestLogOutput],
handler: async (request, context) => {
context.log('HTTP trigger and SQL output binding function processed a request.');
const newLog = {
RequestTimeStamp: Date.now(),
ItemCount: 1,
};
context.extraOutputs.set(sqlRequestLogOutput, newLog);
const body = await request.json();
context.extraOutputs.set(sqlTodoOutput, body);
return { status: 201 };
},
});
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write records to a table

The following example shows a SQL output binding in a function.json file and a PowerShell function that adds records to a table, using data provided in an HTTP POST request as a JSON body.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
```powershell
using namespace System.Net
param($Request)
Write-Host "PowerShell function with SQL Output Binding processed a request."
# Update req_body with the body of the request
$req_body = $Request.Body
# Assign the value we want to pass to the SQL Output binding.
# The -Name value corresponds to the name property in the function.json for the binding
Push-OutputBinding -Name todoItems -Value $req_body
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding in a function.json file and a PowerShell function that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
},
{
"name": "requestLog",
"type": "sql",
"direction": "out",
"commandText": "dbo.RequestLog",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request)
Write-Host "PowerShell function with SQL Output Binding processed a request."
# Update req_body with the body of the request
$req_body = $Request.Body
$new_log = @{
RequestTimeStamp = [DateTime]::Now
ItemCount = 1
}
Push-OutputBinding -Name todoItems -Value $req_body
Push-OutputBinding -Name requestLog -Value $new_log
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

This section contains the following examples:

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write records to a table

The following example shows a SQL output binding in a function.json file and a Python function that adds records to a table, using data provided in an HTTP POST request as a JSON body.

The following is sample python code for the function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="AddToDo")
@app.route(route="addtodo")
@app.sql_output(arg_name="todo",
command_text="[dbo].[ToDo]",
connection_string_setting="SqlConnectionString")
def add_todo(req: func.HttpRequest, todo: func.Out[func.SqlRow]) -> func.HttpResponse:
body = json.loads(req.get_body())
row = func.SqlRow.from_dict(body)
todo.set(row)
return func.HttpResponse(
body=req.get_body(),
status_code=201,
mimetype="application/json"
)
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding in a function.json file and a Python function that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


The following is sample python code for the function_app.py file:

```
from datetime import datetime
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="PostToDo")
@app.route(route="posttodo")
@app.sql_output(arg_name="todoItems",
command_text="[dbo].[ToDo]",
connection_string_setting="SqlConnectionString")
@app.sql_output(arg_name="requestLog",
command_text="[dbo].[RequestLog]",
connection_string_setting="SqlConnectionString")
def add_todo(req: func.HttpRequest, todoItems: func.Out[func.SqlRow], requestLog: func.Out[func.SqlRow]) -> func.HttpResponse:
logging.info('Python HTTP trigger and SQL output binding function processed a request.')
try:
req_body = req.get_json()
rows = func.SqlRowList(map(lambda r: func.SqlRow.from_dict(r), req_body))
except ValueError:
pass
requestLog.set(func.SqlRow({
"RequestTimeStamp": datetime.now().isoformat(),
"ItemCount": 1
}))
if req_body:
todoItems.set(rows)
return func.HttpResponse(
"OK",
status_code=201,
mimetype="application/json"
)
else:
return func.HttpResponse(
"Error accessing request body",
status_code=400
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlAttribute](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/SqlAttribute.cs) attribute to declare the SQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
CommandText |
Required. The name of the table being written to by the binding. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLOutput`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLOutput`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
commandText |
Required. The name of the table being written to by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. |
name |
Required. The unique name of the function binding. |

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.sql()`

method.

| Property | Description |
|---|---|
commandText |
Required. The name of the table being written to by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. Optional keywords in the connection string value are
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required. Must be set to `sql` . |
direction |
Required. Must be set to `out` . |
name |
Required. The name of the variable that represents the entity in function code. |
commandText |
Required. The name of the table being written to by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. Optional keywords in the connection string value are
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The `CommandText`

property is the name of the table where the data is to be stored. The connection string setting name corresponds to the application setting that contains the [connection string](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString) to the Azure SQL or SQL Server instance.

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

The output bindings use the T-SQL [MERGE](/en-us/sql/t-sql/statements/merge-transact-sql) statement which requires [SELECT](/en-us/sql/t-sql/statements/merge-transact-sql#permissions) permissions on the target database.

If an exception occurs when a SQL output binding is executed, then the function code stops executing. This behavior may result in an error code being returned, such as an HTTP trigger returning a 500 error code. If the `IAsyncCollector`

is used in a .NET function, then the function code can handle exceptions throw by the call to `FlushAsync()`

.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-bicep -->

# Quickstart: Create and deploy Azure Functions resources using Bicep

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use Bicep to create a function app in a Flex Consumption plan in Azure, along with its required Azure resources. The function app provides a serverless execution context for your function code executions. The app uses Microsoft Entra ID with managed identities to connect to other Azure resources.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language (DSL) that uses declarative syntax to deploy Azure resources. It provides concise syntax, reliable type safety, and support for code reuse. Bicep offers the best authoring experience for your infrastructure-as-code solutions in Azure.

After you create the function app, you can deploy your Azure Functions project code to that app. A final code deployment step is outside the scope of this quickstart article.

## Prerequisites

### Azure account

Before you begin, you must have an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the Bicep file

The Bicep file used in this quickstart is from an [Azure Quickstart Template](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/main.bicep).

```
/* This Bicep file creates a function app running in a Flex Consumption plan
that connects to Azure Storage by using managed identities with Microsoft Entra ID. */
//********************************************
// Parameters
//********************************************
@description('Primary region for all Azure resources.')
@minLength(1)
param location string = resourceGroup().location
@description('Language runtime used by the function app.')
@allowed(['dotnet-isolated','python','java', 'node', 'powerShell'])
param functionAppRuntime string = 'dotnet-isolated' //Defaults to .NET isolated worker
@description('Target language version used by the function app.')
@allowed(['3.10','3.11', '7.4', '8.0', '9.0', '10', '11', '17', '20'])
param functionAppRuntimeVersion string = '8.0' //Defaults to .NET 8.
@description('The maximum scale-out instance count limit for the app.')
@minValue(40)
@maxValue(1000)
param maximumInstanceCount int = 100
@description('The memory size of instances used by the app.')
@allowed([2048,4096])
param instanceMemoryMB int = 2048
@description('A unique token used for resource name generation.')
@minLength(3)
param resourceToken string = toLower(uniqueString(subscription().id, location))
@description('A globally unique name for your deployed function app.')
param appName string = 'func-${resourceToken}'
//********************************************
// Variables
//********************************************
// Generates a unique container name for deployments.
var deploymentStorageContainerName = 'app-package-${take(appName, 32)}-${take(resourceToken, 7)}'
// Key access to the storage account is disabled by default
var storageAccountAllowSharedKeyAccess = false
// Define the IDs of the roles we need to assign to our managed identities.
var storageBlobDataOwnerRoleId = 'b7e6dc6d-f1e8-4753-8033-0f276bb0955b'
var storageBlobDataContributorRoleId = 'ba92f5b4-2d11-453d-a403-e96b0029c9fe'
var storageQueueDataContributorId = '974c5e8b-45b9-4653-ba55-5f855dd0fb88'
var storageTableDataContributorId = '0a9a7e1f-b9d0-4cc4-a60d-0319b160aaa3'
var monitoringMetricsPublisherId = '3913510d-42f4-4e42-8a64-420c390055eb'
//********************************************
// Azure resources required by your function app.
//********************************************
resource logAnalytics 'Microsoft.OperationalInsights/workspaces@2023-09-01' = {
name: 'log-${resourceToken}'
location: location
properties: any({
retentionInDays: 30
features: {
searchVersion: 1
}
sku: {
name: 'PerGB2018'
}
})
}
resource applicationInsights 'Microsoft.Insights/components@2020-02-02' = {
name: 'appi-${resourceToken}'
location: location
kind: 'web'
properties: {
Application_Type: 'web'
WorkspaceResourceId: logAnalytics.id
DisableLocalAuth: true
}
}
resource storage 'Microsoft.Storage/storageAccounts@2023-05-01' = {
name: 'st${resourceToken}'
location: location
kind: 'StorageV2'
sku: { name: 'Standard_LRS' }
properties: {
accessTier: 'Hot'
allowBlobPublicAccess: false
allowSharedKeyAccess: storageAccountAllowSharedKeyAccess
dnsEndpointType: 'Standard'
minimumTlsVersion: 'TLS1_2'
networkAcls: {
bypass: 'AzureServices'
defaultAction: 'Allow'
}
publicNetworkAccess: 'Enabled'
}
resource blobServices 'blobServices' = {
name: 'default'
properties: {
deleteRetentionPolicy: {}
}
resource deploymentContainer 'containers' = {
name: deploymentStorageContainerName
properties: {
publicAccess: 'None'
}
}
}
}
resource userAssignedIdentity 'Microsoft.ManagedIdentity/userAssignedIdentities@2023-01-31' = {
name: 'uai-data-owner-${resourceToken}'
location: location
}
resource roleAssignmentBlobDataOwner 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Blob Data Owner')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageBlobDataOwnerRoleId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentBlob 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Blob Data Contributor')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageBlobDataContributorRoleId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentQueueStorage 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Queue Data Contributor')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageQueueDataContributorId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentTableStorage 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Table Data Contributor')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageTableDataContributorId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentAppInsights 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, applicationInsights.id, userAssignedIdentity.id, 'Monitoring Metrics Publisher')
scope: applicationInsights
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', monitoringMetricsPublisherId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
//********************************************
// Function app and Flex Consumption plan definitions
//********************************************
resource appServicePlan 'Microsoft.Web/serverfarms@2024-04-01' = {
name: 'plan-${resourceToken}'
location: location
kind: 'functionapp'
sku: {
tier: 'FlexConsumption'
name: 'FC1'
}
properties: {
reserved: true
}
}
resource functionApp 'Microsoft.Web/sites@2024-04-01' = {
name: appName
location: location
kind: 'functionapp,linux'
identity: {
type: 'UserAssigned'
userAssignedIdentities: {
'${userAssignedIdentity.id}':{}
}
}
properties: {
serverFarmId: appServicePlan.id
httpsOnly: true
siteConfig: {
minTlsVersion: '1.2'
}
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storage.properties.primaryEndpoints.blob}${deploymentStorageContainerName}'
authentication: {
type: 'UserAssignedIdentity'
userAssignedIdentityResourceId: userAssignedIdentity.id
}
}
}
scaleAndConcurrency: {
maximumInstanceCount: maximumInstanceCount
instanceMemoryMB: instanceMemoryMB
}
runtime: {
name: functionAppRuntime
version: functionAppRuntimeVersion
}
}
}
resource configAppSettings 'config' = {
name: 'appsettings'
properties: {
AzureWebJobsStorage__accountName: storage.name
AzureWebJobsStorage__credential : 'managedidentity'
AzureWebJobsStorage__clientId: userAssignedIdentity.properties.clientId
APPINSIGHTS_INSTRUMENTATIONKEY: applicationInsights.properties.InstrumentationKey
APPLICATIONINSIGHTS_AUTHENTICATION_STRING: 'ClientId=${userAssignedIdentity.properties.clientId};Authorization=AAD'
}
}
}
```


This deployment file creates these Azure resources needed by a function app that securely connects to Azure services:

: creates your function app.**Microsoft.Web/sites**: creates a serverless Flex Consumption hosting plan for your app.**Microsoft.Web/serverfarms**: creates an Azure Storage account, which is required by Functions.**Microsoft.Storage/storageAccounts**: creates an Application Insights instance for monitoring your app.**Microsoft.Insights/components**: creates a workspace required by Application Insights.**Microsoft.OperationalInsights/workspaces**: creates a user-assigned managed identity that's used by the app to authenticate with other Azure services using Microsoft Entra.**Microsoft.ManagedIdentity/userAssignedIdentities**: creates role assignments to the user-assigned managed identity, which provide the app with least-privilege access when connecting to other Azure services.**Microsoft.Authorization/roleAssignments**

Deployment considerations:

- The storage account is used to store important app data, including the application code deployment package. This deployment creates a storage account that is accessed using Microsoft Entra ID authentication and managed identities. Identity access is granted on a least-permissions basis.
- The Bicep file defaults to creating a C# app that uses .NET 8 in an isolated process. For other languages, use the
`functionAppRuntime`

and`functionAppRuntimeVersion`

parameters to specify the specific language and version on which to run your app. Make sure to select your programming language at the[top](#top)of the article.

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Deploy the Bicep file using either Azure CLI or Azure PowerShell.

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=dotnet-isolated functionAppRuntimeVersion=8.0`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=java functionAppRuntimeVersion=17`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=node functionAppRuntimeVersion=20`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=python functionAppRuntimeVersion=3.11`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=powerShell functionAppRuntimeVersion=7.4`

In this example, replace

`<SUPPORTED_REGION>`

with a region that[supports the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions).When the deployment finishes, you should see a message indicating the deployment succeeded.


## Validate the deployment

Use Azure CLI or Azure PowerShell to validate the deployment.

```
az resource list --resource-group exampleRG
```


## Visit function app welcome page

Use the output from the previous validation step to retrieve the unique name created for your function app.

Open a browser and enter the following URL:

**<https://<appName.azurewebsites.net>**. Make sure to replace**<\appName>**with the unique name created for your function app.When you visit the URL, you should see a page like this:


## Clean up resources

Now that you have deployed a function app and related resources to Azure, can continue to the next step of publishing project code to your app. Otherwise, use these commands to delete the resources, when you no longer need them.

```
az group delete --name exampleRG
```


You can also remove resources by using the [Azure portal](https://portal.azure.com).

## Next steps

You can now deploy a code project to the function app resources you created in Azure.

You can create, verify, and deploy a code project to your new function app from these local environments:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/update-language-versions -->

# Update language stack versions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, support for a language stack is limited to [specific versions](functions-versions#languages). As new versions become available, you might want to update your function apps to take advantage of new features. Support in Functions also ends for older versions and typically aligns with community end-of-support timelines. For more information, see the [language runtime support policy](language-support-policy). For supported versions of various languages, see [Languages by runtime version](supported-languages#languages-by-runtime-version).

To help ensure your function apps continue to receive support, follow the instructions in this article to update them to the latest available versions. The way that you update your function app depends on several factors:

- The language you use to develop your function apps. Make sure to select your programming language at the top of this article.
- The operating system on which your function app runs in Azure: Windows or Linux.
- The
[hosting plan](functions-scale).

Note

This article shows you how to update the .NET version of a function app that uses the [isolated worker model](dotnet-isolated-process-guide). If your function app runs on an older version of .NET and uses the [in-process model](functions-dotnet-class-library), consider the following options:

## Prepare your function app

Before you update the stack configuration for your function app in Azure, complete the tasks in the following sections.

### Review dependencies

Before updating language versions, review these potential dependencies:

**Extension bundles**: Verify that your`host.json`

file references a compatible[extension bundle version](functions-bindings-register#extension-bundles). Version 4.x bundles are recommended for most scenarios.

**Binding extensions**: Update any explicit binding extension references to versions compatible with your new language version.**Package dependencies**: Review and update all package dependencies to versions that support your target language version.**Local tools**: Ensure your local development tools, such as Azure Functions Core Tools, SDKs, and IDEs, support the new language version.

### Verify your function app locally

Test and verify your function app code locally on the new target version.

Use these steps to update the project on your local computer:

Ensure that the

[target version of the .NET SDK is installed](https://dotnet.microsoft.com/download/dotnet).If you're targeting a preview version, see

[Functions guidance for preview .NET versions](dotnet-isolated-process-guide#preview-net-versions)to ensure that the version is supported. Using .NET previews might require more steps.Update your references to the latest versions of

[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/)and[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/).Update your project's target framework to the new version. For C# projects, you must update the

`<TargetFramework>`

element in the*.csproj*file. For more information about your version, see[Target frameworks](/en-us/dotnet/standard/frameworks).Changing your project's target framework might also require changes to parts of your toolchain, outside project code. For example, in Visual Studio Code, you might need to update the

`azureFunctions.deploySubpath`

extension setting in your user settings or your project's*.vscode/settings.json*file. Check for any dependencies on the framework version that exist outside your project code, as part of build steps or a continuous integration and continuous delivery (CI/CD) pipeline.Make any updates to your project code that the new .NET version requires. Check the version's release notes for specific information. You can also use the

[.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview)to help update your code in response to changes across major versions.

After you make those changes, rebuild your project and test it to confirm your function app runs as expected.

### Move to the latest Functions runtime

Make sure your function app runs on the latest version of the Functions runtime (version 4.x). You can determine the runtime version either in the Azure portal or by using the Azure CLI.

Use these steps to determine your Functions runtime version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**.Go to the

**Function runtime settings**tab and check the**Runtime version**value. Your function app should run on version 4.x of the Functions runtime (`~4`

).

If you need to update your function app to version 4.x, see [Migrate apps from Azure Functions version 1.x to version 4.x](migrate-version-1-version-4) or [Migrate apps from Azure Functions version 3.x to version 4.x](migrate-version-3-version-4). Follow the instructions in those articles rather than just changing the `FUNCTIONS_EXTENSION_VERSION`

setting.

### Publish function app updates

If you updated your function app to run correctly on the new version, publish the function app updates before you update the stack configuration for your function app.

Tip

To streamline the update process, minimize downtime for your function apps, and provide a potential version for rollback, publish your updated function app to a staging slot. For more information, see [Azure Functions deployment slots](functions-deployment-slots#add-a-slot).

When you publish your updated function app to a staging slot, make sure to follow the slot-specific update instructions in the rest of this article. You later swap the updated staging slot into production.

### Consider using slots

Before updating your function app's language version, create a [deployment slot](functions-deployment-slots#add-a-slot) to use for testing and deployment. This approach minimizes downtime and provides an easy rollback option if issues occur. The examples in this article use a staging slot named `staging`

.

**Flex Consumption plan**: Slots aren't currently supported. You should first verify your updated code in a non-production function app. When deploying to a running app, you might be able to use the rolling update strategy. For more information, see [Site update strategies in Flex Consumption](flex-consumption-site-updates).

Important

The rolling update strategy is currently in preview and isn't recommended for production apps. Review the current [limitations and considerations](flex-consumption-site-updates#rolling-update-strategy-considerations) before enabling this strategy in any production app.

## Update the stack configuration

The way that you update the stack configuration depends on whether your function app runs on Windows or on Linux in Azure.

When you use a [staging slot](functions-deployment-slots), make sure to target your updates to the correct slot.

Use the following steps to update the Java version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**Java Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**.

Use the following steps to update the .NET version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**.NET Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**.

Use the following steps to update the Node.js version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**Node.js Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**. This change updates theapplication setting.`WEBSITE_NODE_DEFAULT_VERSION`


Use the following steps to update the PowerShell version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**PowerShell Core Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**.

The portal doesn't support Python apps on Windows. Go to the **Linux** tab instead.

Your function app restarts after you update the version.

Note

During the restart, your function app is unavailable for a brief period, typically 30-60 seconds. If you update a production function app directly (without using a staging slot), plan for this downtime during a maintenance window. The restart terminates any in-flight requests, and new requests fail until the app restarts successfully.

## Verify the update

After your function app restarts, verify that the language version update was successful.

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**.On the

**General settings**tab, verify that the language version displays the new version you selected.Select

**Overview**on the side menu and confirm that the**Status**shows as**Running**.

After verifying the version, also verify that your functions work as expected.

## Swap slots

If you use a staging slot to deploy your code project and update your settings, swap the staging slot into production. For more information, see [Swap slots](functions-deployment-slots#swap-slots).

## Troubleshooting

If you experience issues after updating the language version, use the following guidance to resolve common problems:

### Function app doesn't start

**Symptoms:** The function app status shows as **Stopped** or continuously restarts.

**Solutions:**

Check the application logs in the Azure portal:

- Navigate to your function app and select
**Monitoring**>**Log stream**. - Look for error messages related to runtime or language version mismatches.

- Navigate to your function app and select
Verify that all dependencies are compatible with the new language version:

- For .NET, ensure NuGet packages support the target framework.
- For Python, check that package versions in
`requirements.txt`

are compatible. - For Node.js, verify
`package.json`

dependencies support the new Node version.

Check the

[extension bundle version](functions-bindings-register#extension-bundles)in your`host.json`

file. Older bundles might not support newer language versions.

### Functions fail with runtime errors

**Symptoms:** Individual functions fail when triggered, with errors in the logs.

**Solutions:**

Review breaking changes for your language version:

- See
[Breaking changes in .NET](/en-us/dotnet/core/compatibility/breaking-changes)for your target version.

- Review
[Java release notes](https://www.oracle.com/java/technologies/javase-downloads.html)for migration guidance.

- Check
[Node.js release notes](https://nodejs.org/en/about/previous-releases)for breaking changes.

- See
[What's new in Python](https://docs.python.org/3/whatsnew/)for version-specific changes.

- Review
[PowerShell release notes](/en-us/powershell/scripting/whats-new/overview)for changes.

- See
Update binding extensions to versions compatible with your new language version.

Test functions locally with the new language version before redeploying.


### Extension version conflicts

**Symptoms:** Errors that mention "extension" or "binding" version incompatibilities.

**Solutions:**

Update the

[extension bundle](functions-bindings-register#extension-bundles)version in`host.json`

to version 4.x or later.`{ "version": "2.0", "extensionBundle": { "id": "Microsoft.Azure.Functions.ExtensionBundle", "version": "[4.*, 5.0.0)" } }`

For .NET projects that use explicit extension references, update all

`Microsoft.Azure.WebJobs.Extensions.*`

packages to their latest versions.

### Rolling back the update

If you need to revert to the previous language version:

If you used a staging slot:

- Swap the staging slot back to production.
- Update the staging slot back to the previous version for future attempts.

If you updated production directly:

- Follow the same update steps in this article but specify your previous language version.
- Redeploy your previous code version.

Monitor your function app to ensure it returns to normal operation.


Tip

To avoid issues, always test language version updates in a staging slot before applying them to production. Create a backup of your function app configuration before making changes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-trigger -->

# Azure Event Grid trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the function trigger to respond to an event sent by an [Event Grid source](../event-grid/overview). You must have an event subscription to the source to receive events. To learn how to create an event subscription, see [Create a subscription](event-grid-how-tos#create-a-subscription). For information on binding setup and configuration, see the [overview](functions-bindings-event-grid).

Note

Event Grid triggers aren't natively supported in an internal load balancer App Service Environment (ASE). The trigger uses an HTTP request that can't reach the function app without a gateway into the virtual network.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

For an HTTP trigger example, see [Receive events to an HTTP endpoint](../event-grid/receive-events).

The type of the input parameter used with an Event Grid trigger depends on these three factors:

- Functions runtime version
- Binding extension version
- Modality of the C# function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

When running your C# function in an isolated worker process, you need to define a custom type for event properties. The following example defines a `MyEventType`

class.

```
{
public string? Id { get; set; }
public string? Topic { get; set; }
public string? Subject { get; set; }
public string? EventType { get; set; }
public DateTime EventTime { get; set; }
public IDictionary<string, object>? Data { get; set; }
}
```


The following example shows how the custom type is used in both the trigger and an Event Grid output binding:

```
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
var logger = context.GetLogger(nameof(EventGridFunction));
logger.LogInformation(input.Data?.ToString());
var outputEvent = new MyEventType()
{
Id = "unique-id",
Subject = "abc-subject",
Data = new Dictionary<string, object>
{
{ "myKey", "myValue" }
}
};
return outputEvent;
}
```


This section contains the following examples:

The following examples show trigger binding in [Java](functions-reference-java) that use the binding and generate an event, first receiving the event as `String`

and second as a POJO.

### Event Grid trigger, String parameter

```
@FunctionName("eventGridMonitorString")
public void logEvent(
@EventGridTrigger(
name = "event"
)
String content,
final ExecutionContext context) {
context.getLogger().info("Event content: " + content);
}
```


### Event Grid trigger, POJO parameter

This example uses the following POJO, representing the top-level properties of an Event Grid event:

```
import java.util.Date;
import java.util.Map;
public class EventSchema {
public String topic;
public String subject;
public String eventType;
public Date eventTime;
public String id;
public String dataVersion;
public String metadataVersion;
public Map<String, Object> data;
}
```


Upon arrival, the event's JSON payload is de-serialized into the `EventSchema`

POJO for use by the function. This process allows the function to access the event's properties in an object-oriented way.

```
@FunctionName("eventGridMonitor")
public void logEvent(
@EventGridTrigger(
name = "event"
)
EventSchema event,
final ExecutionContext context) {
context.getLogger().info("Event content: ");
context.getLogger().info("Subject: " + event.subject);
context.getLogger().info("Time: " + event.eventTime); // automatically converted to Date by the runtime
context.getLogger().info("Id: " + event.id);
context.getLogger().info("Data: " + event.data);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventGridTrigger`

annotation on parameters whose value would come from Event Grid. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example shows an event grid trigger [TypeScript function](functions-reference-node?tabs=typescript).

```
import { app, EventGridEvent, InvocationContext } from '@azure/functions';
export async function eventGridTrigger1(event: EventGridEvent, context: InvocationContext): Promise<void> {
context.log('Event grid function processed event:', event);
}
app.eventGrid('eventGridTrigger1', {
handler: eventGridTrigger1,
});
```


The following example shows an event grid trigger [JavaScript function](functions-reference-node).

```
const { app } = require('@azure/functions');
app.eventGrid('eventGridTrigger1', {
handler: (event, context) => {
context.log('Event grid function processed event:', event);
},
});
```


The following example shows how to configure an Event Grid trigger binding in the *function.json* file.

```
{
"bindings": [
{
"type": "eventGridTrigger",
"name": "eventGridEvent",
"direction": "in"
}
]
}
```


The Event Grid event is made available to the function via a parameter named `eventGridEvent`

, as shown in the following PowerShell example.

```
param($eventGridEvent, $TriggerMetadata)
# Make sure to pass hashtables to Out-String so they're logged correctly
$eventGridEvent | Out-String | Write-Host
```


The following example shows an Event Grid trigger binding and a Python function that uses the binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="eventGridTrigger")
@app.event_grid_trigger(arg_name="event")
def eventGridTest(event: func.EventGridEvent):
result = json.dumps({
'id': event.id,
'data': event.get_json(),
'topic': event.topic,
'subject': event.subject,
'event_type': event.event_type,
})
logging.info('Python EventGrid trigger processed an event: %s', result)
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [EventGridTrigger](https://github.com/Azure/azure-functions-eventgrid-extension/blob/master/src/EventGridExtension/TriggerBinding/EventGridTriggerAttribute.cs) attribute. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-grid-trigger).

Here's an `EventGridTrigger`

attribute in a method signature:

```
[Function(nameof(EventGridFunction))]
[EventGridOutput(TopicEndpointUri = "MyEventGridTopicUriSetting", TopicKeySetting = "MyEventGridTopicKeySetting")]
public static MyEventType Run([EventGridTrigger] MyEventType input, FunctionContext context)
{
```


## Annotations

The [EventGridTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventgridtrigger) annotation allows you to declaratively configure an Event Grid binding by providing configuration values. See the [example](#example) and [configuration](#configuration) sections for more detail.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. There are no constructor parameters or properties to set in the `EventGridTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Required - must be set to `eventGridTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the parameter that receives the event data. |

See the [Example section](#example) for complete examples.

## Usage

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

The parameter type supported by the Event Grid trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single event, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the event into a plain-old CLR object (POCO) type. |
`string` |
The event as a string. |
1 |

[CloudEvent](/en-us/dotnet/api/azure.messaging.cloudevent)1[EventGridEvent](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridevent)1When you want the function to process a batch of events, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
`CloudEvent[]` 1,`EventGridEvent[]` 1,`string[]` ,`BinaryData[]` 1 |
An array of events from the batch. Each entry represents one event. |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventGrid 3.3.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid/3.3.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The Event Grid event instance is available via the parameter associated to the `EventGridTrigger`

attribute, typed as an `EventSchema`

.

The Event Grid instance is available via the parameter configured in the *function.json* file's `name`

property.

The Event Grid instance is available via the parameter configured in the *function.json* file's `name`

property, typed as `func.EventGridEvent`

.

## Event schema

Data for an Event Grid event is received as a JSON object in the body of an HTTP request. The JSON looks similar to the following example:

```
[{
"topic": "/subscriptions/{subscriptionid}/resourceGroups/eg0122/providers/Microsoft.Storage/storageAccounts/egblobstore",
"subject": "/blobServices/default/containers/{containername}/blobs/blobname.jpg",
"eventType": "Microsoft.Storage.BlobCreated",
"eventTime": "2018-01-23T17:02:19.6069787Z",
"id": "{guid}",
"data": {
"api": "PutBlockList",
"clientRequestId": "{guid}",
"requestId": "{guid}",
"eTag": "0x8D562831044DDD0",
"contentType": "application/octet-stream",
"contentLength": 2248,
"blobType": "BlockBlob",
"url": "https://egblobstore.blob.core.windows.net/{containername}/blobname.jpg",
"sequencer": "000000000000272D000000000003D60F",
"storageDiagnostics": {
"batchId": "{guid}"
}
},
"dataVersion": "",
"metadataVersion": "1"
}]
```


The example shown is an array of one element. Event Grid always sends an array and may send more than one event in the array. The runtime invokes your function once for each array element.

The top-level properties in the event JSON data are the same among all event types, while the contents of the `data`

property are specific to each event type. The example shown is for a blob storage event.

For explanations of the common and event-specific properties, see [Event properties](../event-grid/event-schema#event-properties) in the Event Grid documentation.

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Dispatch an Event Grid event](functions-bindings-event-grid-output)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/deployment-zip-push -->

# Zip deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to deploy your function app project files to Azure from a .zip (compressed) file. You learn how to do a push deployment, both by using Azure CLI and by using the REST APIs. [Azure Functions Core Tools](functions-run-local) also uses these deployment APIs when publishing a local project to Azure.

Zip deployment is also an easy way to [run your functions from a package file in Azure](run-functions-from-deployment-package). It's the default deployment technology in the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans. The [Flex Consumption](flex-consumption-plan) plan doesn't support zip deployment.

Azure Functions has the full range of continuous deployment and integration options that are provided by Azure App Service. For more information, see [Continuous deployment for Azure Functions](functions-continuous-deployment).

To speed up development, you might find it easier to deploy your function app project files directly from a .zip file. The .zip deployment API takes the contents of a .zip file and extracts the contents into the `wwwroot`

folder of your function app. This .zip file deployment uses the same Kudu service that powers continuous integration-based deployments, including:

- Deletion of files that were left over from earlier deployments.
- Deployment customization, including running deployment scripts.
- Deployment logs.
- Syncing function triggers in a
[Consumption plan](functions-scale)function app.

For more information, see the [.zip deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file-or-url).

Important

When you use .zip deployment, any files from the previous deployment are either deleted or updated during a subsequent deployment to your function app. Other files and directories in your function app that weren't part of the previous deployment are maintained.

## Deployment .zip file requirements

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

A zip deployment process extracts the zip archive's files and folders in the `wwwroot`

directory. If you include the parent directory when creating the archive, the system won't find the files it expects to see in `wwwroot`

.

## Deploy by using Azure CLI

You can use Azure CLI to trigger a push deployment. Push deploy a .zip file to your function app by using the [az functionapp deployment source config-zip](/en-us/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip) command. To use this command, you must use Azure CLI version 2.0.21 or later. To see what Azure CLI version you're using, use the `az --version`

command.

In the following command, replace the `<zip_file_path>`

placeholder with the path to the location of your .zip file. Also, replace `<app_name>`

with the unique name of your function app and replace `<resource_group>`

with the name of your resource group.

```
az functionapp deployment source config-zip -g <resource_group> -n \
<app_name> --src <zip_file_path>
```


This command deploys project files from the downloaded .zip file to your function app in Azure. It then restarts the app. To view the list of deployments for this function app, you must use the REST APIs.

When you're using Azure CLI on your local computer, `<zip_file_path>`

is the path to the .zip file on your computer. You can also run Azure CLI in [Azure Cloud Shell](../cloud-shell/overview). When you use Cloud Shell, you must first upload your deployment .zip file to the Azure Files account that's associated with your Cloud Shell. In that case, `<zip_file_path>`

is the storage location that your Cloud Shell account uses. For more information, see [Persist files in Azure Cloud Shell](../cloud-shell/persisting-shell-storage).

## Deploy ZIP file with REST APIs

You can use the [deployment service REST APIs](https://github.com/projectkudu/kudu/wiki/REST-API) to deploy the .zip file to your app in Azure. To deploy, send a POST request to `https://<app_name>.scm.azurewebsites.net/api/zipdeploy`

. The POST request must contain the .zip file in the message body. The deployment credentials for your app are provided in the request by using HTTP BASIC authentication. For more information, see the [.zip push deployment reference](https://github.com/projectkudu/kudu/wiki/Deploying-from-a-zip-file).

For the HTTP BASIC authentication, you need your App Service deployment credentials. To see how to set your deployment credentials, see [Set and reset user-level credentials](../app-service/deploy-configure-credentials#userscope).

### With cURL

The following example uses the cURL tool to deploy a .zip file. Replace the placeholders `<deployment_user>`

, `<zip_file_path>`

, and `<app_name>`

. When prompted by cURL, type in the password.

```
curl -X POST -u <deployment_user> --data-binary "@<zip_file_path>" https://<app_name>.scm.azurewebsites.net/api/zipdeploy
```


This request triggers push deployment from the uploaded .zip file. You can review the current and past deployments by using the `https://<app_name>.scm.azurewebsites.net/api/deployments`

endpoint, as shown in the following cURL example. Again, replace `<app_name>`

with the name of your app and `<deployment_user>`

with the username of your deployment credentials.

```
curl -u <deployment_user> https://<app_name>.scm.azurewebsites.net/api/deployments
```


#### Asynchronous zip deployment

While deploying synchronously, you might receive errors related to connection timeouts. Add `?isAsync=true`

to the URL to deploy asynchronously. You receive a response as soon as the zip file is uploaded with a `Location`

header pointing to the pollable deployment status URL. When polling the URL provided in the `Location`

header, you receive an HTTP 202 (Accepted) response while the process is ongoing and an HTTP 200 (OK) response once the archive has been expanded and the deployment completes successfully.

#### Microsoft Entra authentication

An alternative to using HTTP BASIC authentication for the zip deployment is to use a Microsoft Entra identity. Microsoft Entra identity might be needed if [HTTP BASIC authentication is disabled for the SCM site](../app-service/deploy-configure-credentials#disable-basic-authentication).

A valid Microsoft Entra access token for the user or service principal performing the deployment is required. An access token can be retrieved using the Azure CLI's `az account get-access-token`

command. The access token is used in the Authentication header of the HTTP POST request.

```
curl -X POST \
--data-binary "@<zip_file_path>" \
-H "Authorization: Bearer <access_token>" \
"https://<app_name>.scm.azurewebsites.net/api/zipdeploy"
```


### With PowerShell

The following example uses [Publish-AzWebapp](/en-us/powershell/module/az.websites/publish-azwebapp) upload the .zip file. Replace the placeholders `<group-name>`

, `<app-name>`

, and `<zip-file-path>`

.

```
Publish-AzWebapp -ResourceGroupName <group-name> -Name <app-name> -ArchivePath <zip-file-path>
```


This request triggers push deployment from the uploaded .zip file.

To review the current and past deployments, run the following commands. Again, replace the `<deployment-user>`

, `<deployment-password>`

, and `<app-name>`

placeholders.

```
$username = "<deployment-user>"
$password = "<deployment-password>"
$apiUrl = "https://<app-name>.scm.azurewebsites.net/api/deployments"
$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(("{0}:{1}" -f $username, $password)))
$userAgent = "powershell/1.0"
Invoke-RestMethod -Uri $apiUrl -Headers @{Authorization=("Basic {0}" -f $base64AuthInfo)} -UserAgent $userAgent -Method GET
```


## Deploy by using ARM Template

You can use [ZipDeploy ARM template extension](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy#zipdeploy) to push your .zip file to your function app.

### Example ZipDeploy ARM Template

This template includes both a production and staging slot and deploys to one or the other. Typically, you would use this template to deploy to the staging slot and then swap to get your new zip package running on the production slot.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"parameters": {
"appServiceName": {
"type": "string"
},
"deployToProduction": {
"type": "bool",
"defaultValue": false
},
"slot": {
"type": "string",
"defaultValue": "staging"
},
"packageUri": {
"type": "secureString"
}
},
"resources": [
{
"condition": "[parameters('deployToProduction')]",
"type": "Microsoft.Web/sites/extensions",
"apiVersion": "2021-02-01",
"name": "[format('{0}/ZipDeploy', parameters('appServiceName'))]",
"properties": {
"packageUri": "[parameters('packageUri')]",
"appOffline": true
}
},
{
"condition": "[not(parameters('deployToProduction'))]",
"type": "Microsoft.Web/sites/slots/extensions",
"apiVersion": "2021-02-01",
"name": "[format('{0}/{1}/ZipDeploy', parameters('appServiceName'), parameters('slot'))]",
"properties": {
"packageUri": "[parameters('packageUri')]",
"appOffline": true
}
}
]
}
```


For the initial deployment, you would deploy directly to the production slot. For more information, see [Slot deployments](functions-infrastructure-as-code#slot-deployments).

## Run functions from the deployment package

You can also choose to run your functions directly from the deployment package file. This method skips the deployment step of copying files from the package to the `wwwroot`

directory of your function app. Instead, the Functions runtime mounts the package file, and the contents of the `wwwroot`

directory become read-only.

Zip deployment integrates with this feature, which you can enable by setting the function app setting `WEBSITE_RUN_FROM_PACKAGE`

to a value of `1`

. For more information, see [Run your functions from a deployment package file](run-functions-from-deployment-package).

## Deployment customization

The deployment process assumes that the .zip file that you push contains a ready-to-run app. By default, no customizations are run. To enable the same build processes that you get with continuous integration, add the following to your application settings:

`SCM_DO_BUILD_DURING_DEPLOYMENT=true`


When you use .zip push deployment, this setting is **false** by default. The default is **true** for continuous integration deployments. When set to **true**, your deployment-related settings are used during deployment. You can configure these settings either as app settings or in a .deployment configuration file that's located in the root of your .zip file. For more information, see [Repository and deployment-related settings](https://github.com/projectkudu/kudu/wiki/Configurable-settings#repository-and-deployment-related-settings) in the deployment reference.

## Download your function app files

If you created your functions by using the editor in the Azure portal, you can download your existing function app project as a .zip file in one of these ways:

**From the Azure portal:**Sign in to the

[Azure portal](https://portal.azure.com), and then go to your function app.On the

**Overview**tab, select**Download app content**. Select your download options, and then select**Download**.

The downloaded .zip file is in the correct format to be republished to your function app by using .zip push deployment. The portal download can also add the files needed to open your function app directly in Visual Studio.

**Using REST APIs:**Use the following deployment GET API to download the files from your

`<function_app>`

project:`https://<function_app>.scm.azurewebsites.net/api/zip/site/wwwroot/`

Including

`/site/wwwroot/`

makes sure your zip file includes only the function app project files and not the entire site. If you aren't already signed in to Azure, you are asked to do so.

You can also download a .zip file from a GitHub repository. When you download a GitHub repository as a .zip file, GitHub adds an extra folder level for the branch. This extra folder level means that you can't deploy the .zip file directly as you downloaded it from GitHub. If you're using a GitHub repository to maintain your function app, you should use [continuous integration](functions-continuous-deployment) to deploy your app.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-access-azure-sql-with-managed-identity -->

# Tutorial: Connect a function app to Azure SQL with managed identity and SQL bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides a [managed identity](../active-directory/managed-identities-azure-resources/overview), which is a turn-key solution for securing access to [Azure SQL Database](/en-us/azure/sql-database/) and other Azure services. Managed identities make your app more secure by eliminating secrets from your app, such as credentials in the connection strings. In this tutorial, you'll add managed identity to an Azure Function that utilizes [Azure SQL bindings](functions-bindings-azure-sql). A sample Azure Function project with SQL bindings is available in the [ToDo backend example](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/).

When you're finished with this tutorial, your Azure Function will connect to Azure SQL database without the need of username and password.

An overview of the steps you'll take:

## Grant database access to Microsoft Entra user

First enable Microsoft Entra authentication to SQL database by assigning a Microsoft Entra user as the Active Directory admin of the server. This user is different from the Microsoft account you used to sign up for your Azure subscription. It must be a user that you created, imported, synced, or invited into Microsoft Entra ID. For more information on allowed Microsoft Entra users, see [Microsoft Entra features and limitations in SQL database](/en-us/azure/azure-sql/database/authentication-aad-overview#azure-ad-features-and-limitations).

Enabling Microsoft Entra authentication can be completed via the Azure portal, PowerShell, or Azure CLI. Directions for Azure CLI are below and information completing this via Azure portal and PowerShell is available in the [Azure SQL documentation on Microsoft Entra authentication](/en-us/azure/azure-sql/database/authentication-aad-configure).

If your Microsoft Entra tenant doesn't have a user yet, create one by following the steps at

[Add or delete users using Microsoft Entra ID](../active-directory/fundamentals/add-users-azure-active-directory).Find the object ID of the Microsoft Entra user using the

and replace`az ad user list`

*<user-principal-name>*. The result is saved to a variable.For Azure CLI 2.37.0 and newer:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].id --output tsv)`

For older versions of Azure CLI:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].objectId --output tsv)`

Tip

To see the list of all user principal names in Microsoft Entra ID, run

`az ad user list --query [].userPrincipalName`

.Add this Microsoft Entra user as an Active Directory admin using

command in the Cloud Shell. In the following command, replace`az sql server ad-admin create`

*<server-name>*with the server name (without the`.database.windows.net`

suffix).`az sql server ad-admin create --resource-group myResourceGroup --server-name <server-name> --display-name ADMIN --object-id $azureaduser`


For more information on adding an Active Directory admin, see [Provision a Microsoft Entra administrator for your server](/en-us/azure/azure-sql/database/authentication-aad-configure#provision-azure-ad-admin-sql-database)

## Enable system-assigned managed identity on Azure Function

In this step we'll add a system-assigned identity to the Azure Function. In later steps, this identity will be given access to the SQL database.

To enable system-assigned managed identity in the Azure portal:

- Create an Azure Function in the portal as you normally would. Navigate to it in the portal.
- Scroll down to the Settings group in the left navigation.
- Select Identity.
- Within the System assigned tab, switch Status to On. Click Save.


For information on enabling system-assigned managed identity through Azure CLI or PowerShell, check out more information on [using managed identities with Azure Functions](../app-service/overview-managed-identity?tabs=dotnet&toc=/azure/azure-functions/toc.json#add-a-system-assigned-identity).

Tip

For user-assigned managed identity, switch to the User Assigned tab. Click Add and select a Managed Identity. For more information on creating user-assigned managed identity, see the [Manage user-assigned managed identities](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities).

## Grant SQL database access to the managed identity

In this step we'll connect to the SQL database with a Microsoft Entra user account and grant the managed identity access to the database.

Open your preferred SQL tool and login with a Microsoft Entra user account (such as the Microsoft Entra user we assigned as administrator). This can be accomplished in Cloud Shell with the SQLCMD command.

`sqlcmd -S <server-name>.database.windows.net -d <db-name> -U <aad-user-name> -P "<aad-password>" -G -l 30`

In the SQL prompt for the database you want, run the following commands to grant permissions to your function. For example,

`CREATE USER [<identity-name>] FROM EXTERNAL PROVIDER; ALTER ROLE db_datareader ADD MEMBER [<identity-name>]; ALTER ROLE db_datawriter ADD MEMBER [<identity-name>]; GO`

*<identity-name>*is the name of the managed identity in Microsoft Entra ID. If the identity is system-assigned, the name is always the same as the name of your Function app.

## Configure Azure Function SQL connection string

In the final step we'll configure the Azure Function SQL connection string to use Microsoft Entra managed identity authentication.

The connection string setting name is identified in our Functions code as the binding attribute "ConnectionStringSetting", as seen in the SQL input binding [attributes and annotations](functions-bindings-azure-sql-input?pivots=programming-language-csharp#attributes).

In the application settings of our Function App the SQL connection string setting should be updated to follow this format:

`Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb`


*testdb* is the name of the database we're connecting to and *demo.database.windows.net* is the name of the server we're connecting to.

Tip

For user-assigned managed identity, use `Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ClientIdOfManagedIdentity; Database=testdb`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-encrypt-at-rest-using-cmk -->

# Encrypt your application data at rest using customer-managed keys

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Encrypting your function app's application data at rest requires an Azure Storage Account and an Azure Key Vault. These services are used when you run your app from a deployment package.

[Azure Storage provides encryption at rest](../storage/common/storage-service-encryption). You can use system-provided keys or your own, customer-managed keys. This is where your application data is stored when it's not running in a function app in Azure.[Running from a deployment package](run-functions-from-deployment-package)is a deployment feature of App Service. It allows you to deploy your site content from an Azure Storage Account using a Shared Access Signature (SAS) URL.[Key Vault references](../app-service/app-service-key-vault-references)are a security feature of App Service. It allows you to import secrets at runtime as application settings. Use this to encrypt the SAS URL of your Azure Storage Account.

## Set up encryption at rest

### Create an Azure Storage account

First, [create an Azure Storage account](../storage/common/storage-account-create) and [encrypt it with customer managed keys](../storage/common/customer-managed-keys-overview). Once the storage account is created, use the [Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer) to upload package files.

Next, use the Storage Explorer to [generate an SAS](../vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows#generate-a-sas-in-storage-explorer).

Note

Save this SAS URL, this is used later to enable secure access of the deployment package at runtime.

### Configure running from a package from your storage account

Once you upload your file to Blob storage and have an SAS URL for the file, set the `WEBSITE_RUN_FROM_PACKAGE`

application setting to the SAS URL. The following example does it by using Azure CLI:

```
az webapp config appsettings set --name <app-name> --resource-group <resource-group-name> --settings WEBSITE_RUN_FROM_PACKAGE="<your-SAS-URL>"
```


Adding this application setting causes your function app to restart. After the app has restarted, browse to it and make sure that the app has started correctly using the deployment package. If the application didn't start correctly, see the [Run from package troubleshooting guide](run-functions-from-deployment-package#troubleshooting).

### Encrypt the application setting using Key Vault references

Now you can replace the value of the `WEBSITE_RUN_FROM_PACKAGE`

application setting with a Key Vault reference to the SAS-encoded URL. This keeps the SAS URL encrypted in Key Vault, which provides an extra layer of security.

Use the following

command to create a Key Vault instance.`az keyvault create`

`az keyvault create --name "Contoso-Vault" --resource-group <group-name> --location eastus`

Follow

[these instructions to grant your app access](../app-service/app-service-key-vault-references#grant-your-app-access-to-a-key-vault)to your key vault:Use the following

command to add your external URL as a secret in your key vault:`az keyvault secret set`

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Use the following

command to create the`az webapp config appsettings set`

`WEBSITE_RUN_FROM_PACKAGE`

application setting with the value as a Key Vault reference to the external URL:`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

Updating this application setting causes your function app to restart. After the app has restarted, browse to it make sure it has started correctly using the Key Vault reference.

## How to rotate the access token

It is best practice to periodically rotate the SAS key of your storage account. To ensure the function app does not inadvertently lose access, you must also update the SAS URL in Key Vault.

Rotate the SAS key by navigating to your storage account in the Azure portal. Under

**Settings**>**Access keys**, select the icon to rotate the SAS key.Copy the new SAS URL, and use the following command to set the updated SAS URL in your key vault:

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Update the key vault reference in your application setting to the new secret version:

`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

## How to revoke the function app's data access

There are two methods to revoke the function app's access to the storage account.

### Rotate the SAS key for the Azure Storage account

If the SAS key for the storage account is rotated, the function app will no longer have access to the storage account, but it will continue to run with the last downloaded version of the package file. Restart the function app to clear the last downloaded version.

### Remove the function app's access to Key Vault

You can revoke the function app's access to the site data by disabling the function app's access to Key Vault. To do this, remove the access policy for the function app's identity. This is the same identity you created earlier while configuring key vault references.

## Summary

Your application files are now encrypted at rest in your storage account. When your function app starts, it retrieves the SAS URL from your key vault. Finally, the function app loads the application files from the storage account.

If you need to revoke the function app's access to your storage account, you can either revoke access to the key vault or rotate the storage account keys, both of which invalidate the SAS URL.

## Frequently Asked Questions

### Is there any additional charge for running my function app from the deployment package?

Only the cost associated with the Azure Storage Account and any applicable egress charges.

### How does running from the deployment package affect my function app?

- Running your app from the deployment package makes
`wwwroot/`

read-only. Your app receives an error when it attempts to write to this directory. - TAR and GZIP formats are not supported.
- This feature is not compatible with local cache.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-private-site-access -->

# Tutorial: Establish Azure Functions private site access

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to enable [private site access](functions-networking-options#private-endpoints) with Azure Functions. By using private site access, you can require that your function code is only triggered from a specific virtual network.

Private site access is useful in scenarios when access to the function app needs to be limited to a specific virtual network. For example, the function app may be applicable to only employees of a specific organization, or services which are within the specified virtual network (such as another Azure Function, Azure Virtual Machine, or an AKS cluster).

If a Functions app needs to access Azure resources within the virtual network, or connected via [service endpoints](../virtual-network/virtual-network-service-endpoints-overview), then [virtual network integration](functions-create-vnet) is needed.

In this tutorial, you learn how to configure private site access for your function app:

- Create a virtual machine
- Create an Azure Bastion service
- Create an Azure Functions app
- Configure a virtual network service endpoint
- Create and deploy an Azure Function
- Invoke the function from outside and within the virtual network

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

## Topology

The following diagram shows the architecture of the solution to be created:

## Prerequisites

For this tutorial, it's important that you understand IP addressing and subnetting. You can start with [this article that covers the basics of addressing and subnetting](https://support.microsoft.com/help/164015/understanding-tcp-ip-addressing-and-subnetting-basics). Many more articles and videos are available online.

## Sign in to Azure portal

Sign in to the [Azure portal](https://portal.azure.com).

## Create a virtual machine

The first step in this tutorial is to create a new virtual machine inside a virtual network. The virtual machine will be used to access your function once you've restricted its access to only be available from within the virtual network.

Select the

**Create a resource**button.In the search field, type

**Windows Server**, and select**Windows Server**in the search results.Select

**Windows Server 2019 Datacenter**from the list of Windows Server options, and press the**Create**button.In the

*Basics*tab, use the VM settings as specified in the table below the image:Setting Suggested value Description *Subscription*Your subscription The subscription under which your resources are created. *Resource group*myResourceGroup Choose the resource group to contain all the resources for this tutorial. Using the same resource group makes it easier to clean up resources when you're done with this tutorial. *Virtual machine name*myVM The VM name needs to be unique in the resource group *Region*(US) North Central US Choose a region near you or near the functions to be accessed. *Public inbound ports*None Select **None**to ensure there is no inbound connectivity to the VM from the internet. Remote access to the VM will be configured via the Azure Bastion service.Choose the

*Networking*tab and select**Create new**to configure a new virtual network.In

*Create virtual network*, use the settings in the table below the image:Setting Suggested value Description *Name*myResourceGroup-vnet You can use the default name generated for your virtual network. *Address range*10.10.0.0/16 Use a single address range for the virtual network. *Subnet name*Tutorial Name of the subnet. *Address range*(subnet)10.10.1.0/24 The subnet size defines how many interfaces can be added to the subnet. This subnet is used by the VM. A /24 subnet provides 254 host addresses. Select

**OK**to create the virtual network.Back in the

*Networking*tab, ensure**None**is selected for*Public IP*.Choose the

*Management*tab, then in*Diagnostic storage account*, choose**Create new**to create a new Storage account.Leave the default values for the

*Identity*,*Auto-shutdown*, and*Backup*sections.Select

*Review + create*. After validation completes, select**Create**. The VM create process takes a few minutes.

## Configure Azure Bastion

[Azure Bastion](https://azure.microsoft.com/services/azure-bastion/) is a fully managed Azure service which provides secure RDP and SSH access to virtual machines directly from the Azure portal. Using the Azure Bastion service removes the need to configure network settings related to RDP access.

In the portal, choose

**Add**at the top of the resource group view.In the search field, type

**Bastion**.Select

**Bastion**in the search results.Select

**Create**to begin the process of creating a new Azure Bastion resource. You will notice an error message in the*Virtual network*section as there is not yet an AzureBastionSubnet subnet. The subnet is created in the following steps. Use the settings in the table below the image:Setting Suggested value Description *Name*myBastion The name of the new Bastion resource *Region*North Central US Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.*Virtual network*myResourceGroup-vnet The virtual network in which the Bastion resource will be created in *Subnet*AzureBastionSubnet The subnet in your virtual network to which the new Bastion host resource will be deployed. You must create a subnet using the name value **AzureBastionSubnet**. This value lets Azure know which subnet to deploy the Bastion resources to. You must use a subnet of at least**/27**or larger (/27, /26, and so on).Note

For a detailed, step-by-step guide to creating an Azure Bastion resource, refer to the

[Create an Azure Bastion host](../bastion/tutorial-create-host-portal)tutorial.Create a subnet in which Azure can provision the Azure Bastion host. Choosing

**Manage subnet configuration**opens a new pane where you can define a new subnet. Choose**+ Subnet**to create a new subnet.The subnet must be of the name

**AzureBastionSubnet**and the subnet prefix must be at least**/27**. Select**OK**to create the subnet.On the

*Create a Bastion*page, select the newly created**AzureBastionSubnet**from the list of available subnets.Select

**Review & Create**. Once validation completes, select**Create**. It will take a few minutes for the Azure Bastion resource to be created.

## Create an Azure Functions app

The next step is to create a function app in Azure using the [Consumption plan](consumption-plan). You deploy your function code to this resource later in the tutorial.

In the portal, choose

**Add**at the top of the resource group view.Select

**Compute > Function App**On the

*Basics*section, use the function app settings as specified in the table below.Setting Suggested value Description *Resource Group*myResourceGroup Choose the resource group to contain all the resources for this tutorial. Using the same resource group for the function app and VM makes it easier to clean up resources when you're done with this tutorial. *Function App name*Globally unique name Name that identifies your new function app. Valid characters are a-z (case insensitive), 0-9, and -. *Publish*Code Option to publish code files or a Docker container. *Runtime stack*Preferred language Choose a runtime that supports your favorite function programming language. *Region*North Central US Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.Select the

**Next: Hosting >**button.For the

*Hosting*section, select the proper*Storage account*,*Operating system*, and*Plan*as described in the following table.Setting Suggested value Description *Storage account*Globally unique name Create a storage account used by your function app. Storage account names must be between 3 and 24 characters in length and may contain numbers and lowercase letters only. You can also use an existing account, which must meet the [storage account requirements](storage-considerations#storage-account-requirements).*Operating system*Preferred operating system An operating system is pre-selected for you based on your runtime stack selection, but you can change the setting if necessary. *Plan*Consumption The [hosting plan](functions-scale)dictates how the function app is scaled and resources available to each instance.Select

**Review + Create**to review the app configuration selections.Select

**Create**to provision and deploy the function app.

## Configure access restrictions

The next step is to configure [access restrictions](../app-service/app-service-ip-restrictions) to ensure only resources on the virtual network can invoke the function.

[Private site](functions-networking-options#private-endpoints) access is enabled by creating an Azure Virtual Network [service endpoint](../virtual-network/virtual-network-service-endpoints-overview) between the function app and the specified virtual network. Access restrictions are implemented via service endpoints. Service endpoints ensure only traffic originating from within the specified virtual network can access the designated resource. In this case, the designated resource is the Azure Function.

Within the function app, select the

**Networking**link under the*Settings*section header.The

*Networking*page is the starting point to configure Azure Front Door, the Azure CDN, and also Access Restrictions.Select

**Configure Access Restrictions**to configure private site access.On the

*Access Restrictions*page, you see only the default restriction in place. The default doesn't place any restrictions on access to the function app. Select**Add rule**to create a private site access restriction configuration.In the

*Add Access Restriction*pane, provide a*Name*,*Priority*, and*Description*for the new rule.Select

**Virtual Network**from the*Type*drop-down box, then select the previously created virtual network, and then select the**Tutorial**subnet.Note

It may take several minutes to enable the service endpoint.

The

*Access Restrictions*page now shows that there is a new restriction. It may take a few seconds for the*Endpoint status*to change from Disabled through Provisioning to Enabled.Important

Each function app has an

[Advanced Tool (Kudu) site](../app-service/app-service-ip-restrictions#restrict-access-to-an-scm-site)that is used to manage function app deployments. This site is accessed from a URL like:`<FUNCTION_APP_NAME>.scm.azurewebsites.net`

. Enabling access restrictions on the Kudu site prevents the deployment of the project code from a local developer workstation, and then an agent is needed within the virtual network to perform the deployment.

## Access the functions app

Return to the previously created function app. In the

*Overview*section, copy the URL.If you try to access the function app now from your computer outside of your virtual network, you'll receive an HTTP 403 page indicating that access is forbidden.

Return to the resource group and select the previously created virtual machine. In order to access the site from the VM, you need to connect to the VM via the Azure Bastion service.

Select

**Connect**and then choose**Bastion**.Provide the required username and password to log into the virtual machine.

Note

For enhanced security, you should require Microsoft Entra authentication to access your virtual machines in Azure.

Select

**Connect**. A new browser window will pop up to allow you to interact with the virtual machine. It's possible to access the site from the web browser on the VM because the VM is accessing the site through the virtual network. While the site is only accessible from within the designated virtual network, a public DNS entry remains.

## Create a function

The next step in this tutorial is to create an HTTP-triggered Azure Function. Invoking the function via an HTTP GET or POST should result in a response of "Hello, {name}".

Follow one of the following quickstarts to create and deploy your Azure Functions app.

When publishing your Azure Functions project, choose the function app resource that you created earlier in this tutorial.

Verify the function is deployed.


## Invoke the function directly

In order to test access to the function, you need to copy the function URL. Select the deployed function, and then select

**Get Function Url**. Then click the**Copy**button to copy the URL to your clipboard.Paste the URL into a web browser. When you now try to access the function app from a computer outside of your virtual network, you receive an HTTP 403 response indicating access to the app is forbidden.


## Invoke the function from the virtual network

Accessing the function via a web browser (by using the Azure Bastion service) on the configured VM on the virtual network results in success!

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-errors -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-error-pages -->

# Azure Functions error handling and retries

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Handling errors in Azure Functions helps you avoid lost data, avoid missed events, and monitor the health of your application. It's also an important way to help you understand the retry behaviors of event-based triggers.

This article describes general strategies for error handling and the available retry strategies.

Important

The preview of retry policy support for certain triggers was removed in December 2022. Retry policies for supported triggers are now in general availability (GA). The [Retries](#retries) section of this article lists extensions that currently support retry policies.

## Handling errors

Errors that occur in an Azure function can come from:

- Use of built-in Azure Functions
[triggers and bindings](functions-triggers-bindings). - Calls to APIs of underlying Azure services.
- Calls to REST endpoints.
- Calls to client libraries, packages, or non-Microsoft APIs.

To avoid loss of data or missed messages, you should practice good error handling. This table describes some recommended error-handling practices and provides links to more information:

| Recommendation | Details |
|---|---|
| Enable Application Insights | Azure Functions integrates with Application Insights to collect error data, performance data, and runtime logs. Use Application Insights to discover and better understand errors that occur in your function executions. To learn more, see
|

[Binding error codes](#binding-error-codes)in this article. Depending on your specific retry strategy, you might also raise a new exception to run the function again.[Retries](#retries)in this article.[Designing Azure Functions for identical input](functions-idempotent).Tip

When you use output bindings, you can't handle errors that occur from accessing the remote service. Because of this behavior, you should validate all data passed to your output bindings to avoid raising any known exceptions. If you must be able to handle such exceptions in your function code, you should access the remote service by using the client SDK instead of relying on output bindings.

## Retries

Two kinds of retries are available for your functions:

- Built-in retry behaviors of individual trigger extensions
- Retry policies that the Azure Functions runtime provides

The following table indicates which triggers support retries and where the retry behavior is configured. It also links to more information about errors that come from the underlying services.

| Trigger/binding | Retry source | Configuration |
|---|---|---|
| Azure Cosmos DB |
|

[Binding extension](functions-bindings-storage-blob-trigger#poison-blobs)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](../event-grid/delivery-and-retry)[Retry policies](#retry-policies)[Retry policies](#retry-policies)[Binding extension](functions-bindings-storage-queue-trigger#poison-messages)[host.json](functions-bindings-storage-queue#host-json)[Binding extension](functions-bindings-rabbitmq-trigger#dead-letter-queues)[Dead letter queue](https://www.rabbitmq.com/dlx.html)[Binding extension](functions-bindings-service-bus-trigger)[host.json](functions-bindings-service-bus#hostjson-settings)*[Retry policies](#retry-policies)* Requires version 5.x of the Azure Service Bus extension. In older extension versions, the [Service Bus dead letter queue](../service-bus-messaging/service-bus-dead-letter-queues#maximum-delivery-count) implements retry behaviors.

## Retry policies

With Azure Functions, you can define retry policies for specific trigger types. The runtime enforces these retry policies. The following trigger types currently support retry policies:

Retry support is the same for both v1 and v2 Python programming models.

Retry policies aren't supported in version 1.x of the Azure Functions runtime.

The retry policy tells the runtime to rerun a failed execution until either successful completion occurs or the maximum number of retries is reached.

A retry policy is evaluated when a function that a supported trigger type executes raises an uncaught exception. As a best practice, you should catch all exceptions in your code and raise new exceptions for any errors that you want to result in a retry.

Important

Event Hubs checkpoints aren't written until after the retry policy for the execution finishes. Because of this behavior, progress on the specific partition is paused until the current batch finishes processing. For more information, see [Reliable event processing with Azure Functions and Event Hubs](functions-reliable-event-processing).

Version 5.x of the Event Hubs extension supports extra retry capabilities for interactions between the Azure Functions host and the event hub. For more information, see `clientRetryOptions`

in the [Event Hubs host.json reference](functions-bindings-event-hubs#host-json).

### Retry strategies

You can configure two retry strategies that are supported by policy:

A specified amount of time is allowed to elapse between each retry.

When you use a Consumption plan, you're billed only for the time that your function code is running. You aren't billed for the wait time between executions in either of these retry strategies.

### Maximum retry counts

You can configure the maximum number of times that a function execution is retried before eventual failure. The current retry count is stored in the memory of the instance.

It's possible for an instance to have a failure between retry attempts. When an instance fails during a retry policy, the retry count is lost. When there are instance failures, the Event Hubs trigger can resume processing and retry the batch on a new instance, with the retry count reset to zero. The timer trigger doesn't resume on a new instance.

This behavior means that the maximum retry count is a best effort. In some rare cases, an execution could be retried more than the requested maximum number of times. For timer triggers, the retries can be less than the requested maximum number.

### Retry examples

Examples are provided for both fixed delay and exponential backoff strategies. To see examples for a specific strategy, you must first select that strategy on the previous tab.

Function-level retries are supported with the following NuGet packages:

[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk)version 1.9.0 and later[Microsoft.Azure.Functions.Worker.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs)version 5.2.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Kafka](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Kafka)version 3.8.0 and later[Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer)version 4.2.0 and later

```
[Function(nameof(TimerFunction))]
[FixedDelayRetry(5, "00:00:10")]
public static void Run([TimerTrigger("0 */5 * * * *")] TimerInfo timerInfo,
FunctionContext context)
{
var logger = context.GetLogger(nameof(TimerFunction));
logger.LogInformation($"Function Ran. Next timer schedule = {timerInfo.ScheduleStatus?.Next}");
}
```


| Property | Description |
|---|---|
`MaxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`DelayInterval` |
The delay used between retries. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a retry policy defined in the `function.json`

file:

```
{
"disabled": false,
"bindings": [
{
....
}
],
"retry": {
"strategy": "fixedDelay",
"maxRetryCount": 4,
"delayInterval": "00:00:10"
}
}
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
const { app } = require('@azure/functions');
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: (myTimer, context) => {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
},
});
```


The way that you define the retry policy for the trigger depends on your Node.js version:

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTriggerWithRetry(myTimer: Timer, context: InvocationContext): Promise<void> {
if (context.retryContext?.retryCount < 2) {
throw new Error('Retry!');
} else {
context.log('Timer function processed request.');
}
}
app.timer('timerTriggerWithRetry', {
schedule: '0 */5 * * * *',
retry: {
strategy: 'fixedDelay',
delayInterval: {
seconds: 10,
},
maxRetryCount: 4,
},
handler: timerTriggerWithRetry,
});
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixedDelay` and `exponentialBackoff` . |
`maxRetryCount` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delayInterval` |
The delay used between retries when you're using a `fixedDelay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimumInterval` |
The minimum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximumInterval` |
The maximum retry delay when you're using an `exponentialBackoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

Here's an example of a timer trigger function that uses a fixed-delay retry strategy:

```
import logging
from azure.functions import AuthLevel, Context, FunctionApp, TimerRequest
app = FunctionApp(http_auth_level=AuthLevel.ANONYMOUS)
@app.timer_trigger(schedule="*/1 * * * * *", arg_name="mytimer",
run_on_startup=False,
use_monitor=False)
@app.retry(strategy="fixed_delay", max_retry_count="3",
delay_interval="00:00:01")
def mytimer(mytimer: TimerRequest, context: Context) -> None:
logging.info(f'Current retry count: {context.retry_context.retry_count}')
if context.retry_context.retry_count == \
context.retry_context.max_retry_count:
logging.info(
f"Max retries of {context.retry_context.max_retry_count} for "
f"function {context.function_name} has been reached")
else:
raise Exception("This is a retryable exception")
```


You can set these properties on retry policy definitions:

| Property | Description |
|---|---|
`strategy` |
Required. The retry strategy to use. Valid values are `fixed_delay` and `exponential_backoff` . |
`max_retry_count` |
Required. The maximum number of retries allowed per function execution. A value of `-1` means to retry indefinitely. |
`delay_interval` |
The delay used between retries when you're using a `fixed_delay` strategy. Specify it as a string with the format `HH:mm:ss` . |
`minimum_interval` |
The minimum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |
`maximum_interval` |
The maximum retry delay when you're using an `exponential_backoff` strategy. Specify it as a string with the format `HH:mm:ss` . |

```
@FunctionName("TimerTriggerJava1")
@FixedDelayRetry(maxRetryCount = 4, delayInterval = "00:00:10")
public void run(
@TimerTrigger(name = "timerInfo", schedule = "0 */5 * * * *") String timerInfo,
final ExecutionContext context
) {
context.getLogger().info("Java Timer trigger function executed at: " + LocalDateTime.now());
}
```


## Binding error codes

When you're integrating with Azure services, errors might originate from the APIs of the underlying services. Information that relates to binding-specific errors is available in the "Exceptions and return codes" sections of the following articles:

[Azure Cosmos DB](/en-us/rest/api/cosmos-db/http-status-codes-for-cosmosdb)[Blob Storage](functions-bindings-storage-blob-output#exceptions-and-return-codes)[Event Grid](../event-grid/troubleshoot-errors)[Event Hubs](functions-bindings-event-hubs-output#exceptions-and-return-codes)[IoT Hub](functions-bindings-event-iot-output#exceptions-and-return-codes)[Notification Hubs](functions-bindings-notification-hubs#exceptions-and-return-codes)[Queue Storage](functions-bindings-storage-queue-output#exceptions-and-return-codes)[Service Bus](functions-bindings-service-bus-output#exceptions-and-return-codes)[Table Storage](functions-bindings-storage-table-output#exceptions-and-return-codes)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger -->

# Azure Cosmos DB trigger for Azure Functions 2.x and higher

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes new and updated items, not including updates from deletions. For an end-to-end scenario that uses the Azure Cosmos DB trigger, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Cosmos DB scaling decisions for the Consumption and Premium plans are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This article supports both programming models.

## Example

The usage of the trigger depends on the extension package version and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

An in-process class library is a compiled C# function runs in the same process as the Functions runtime.

The following examples depend on the extension version for the given C# mode.

Apps using [Azure Cosmos DB extension version 4.x](functions-bindings-cosmosdb-v2?tabs=extensionv4) or higher have different attribute properties, which are shown here. This example refers to a simple `ToDoItem`

type.

```
namespace CosmosDBSamplesV2
{
// Customize the model with your own desired properties
public class ToDoItem
{
public string id { get; set; }
public string Description { get; set; }
}
}
```


```
using System.Collections.Generic;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "databaseName",
containerName: "containerName",
Connection = "CosmosDBConnectionSetting",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)]IReadOnlyList<ToDoItem> input, ILogger log)
{
if (input != null && input.Count > 0)
{
log.LogInformation("Documents modified " + input.Count);
log.LogInformation("First document Id " + input[0].id);
}
}
}
}
```


The following example shows a [C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using Microsoft.Extensions.Logging;
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
ILogger log)
{
if (documents != null && documents.Count > 0)
{
log.LogInformation($"Documents modified: {documents.Count}");
log.LogInformation($"First document Id: {documents[0].Id}");
}
}
}
}
```


This example refers to a simple `ToDoItem`

type:

```
public class ToDoItem
{
public string? Id { get; set; }
public string? Description { get; set; }
}
```


The following function is invoked when there are inserts or updates in the specified database and collection.

```
[Function("CosmosTrigger")]
public void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
containerName:"TriggerItems",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<ToDoItem> todoItems,
FunctionContext context)
{
if (todoItems is not null && todoItems.Any())
{
foreach (var doc in todoItems)
{
_logger.LogInformation("ToDoItem: {desc}", doc.Description);
}
}
}
```


The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


An `IReadOnlyList<T>`

is used as the Azure Cosmos DB trigger binding parameter in the following example:

```
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
```


This example requires the following `using`

statements:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
```


This function is invoked when there are inserts or updates in the specified database and container.

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

```
@FunctionName("CosmosDBTriggerFunction")
public void run(
@CosmosDBTrigger(
name = "items",
databaseName = "ToDoList",
containerName = "Items",
leaseContainerName="leases",
connection = "AzureCosmosDBConnection",
createLeaseContainerIfNotExists = true
)
Object inputItem,
final ExecutionContext context
) {
context.getLogger().info("Items modified: " + inputItems.size());
}
```


```
@FunctionName("cosmosDBMonitor")
public void cosmosDbProcessor(
@CosmosDBTrigger(name = "items",
databaseName = "ToDoList",
collectionName = "Items",
leaseCollectionName = "leases",
createLeaseCollectionIfNotExists = true,
connectionStringSetting = "AzureCosmosDBConnection") String[] items,
final ExecutionContext context ) {
context.getLogger().info(items.length + "item(s) is/are changed.");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters whose value would come from Azure Cosmos DB. This annotation can be used with native Java types, plain-old Java objects (POJOs), or nullable values using `Optional<T>`

.

The following example shows an Azure Cosmos DB trigger [TypeScript function](functions-reference-node?tabs=typescript). The function writes log messages when Azure Cosmos DB records are added or modified.

```
import { app, InvocationContext } from '@azure/functions';
export async function cosmosDBTrigger1(documents: unknown[], context: InvocationContext): Promise<void> {
context.log(`Cosmos DB function processed ${documents.length} documents`);
}
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: cosmosDBTrigger1,
});
```


TypeScript samples aren't documented for model v3.

The following example shows an Azure Cosmos DB trigger [JavaScript function](functions-reference-node). The function writes log messages when Azure Cosmos DB records are added or modified.

```
const { app } = require('@azure/functions');
app.cosmosDB('cosmosDBTrigger1', {
connection: '<connection-app-setting>',
databaseName: 'Tasks',
containerName: 'Items',
createLeaseContainerIfNotExists: true,
handler: (documents, context) => {
context.log(`Cosmos DB function processed ${documents.length} documents`);
},
});
```


The following example shows an Azure Cosmos DB trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function writes log messages when Azure Cosmos DB records are added or modified.

Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the JavaScript code:

```
module.exports = async function (context, documents) {
context.log('First document Id modified : ', documents[0].id);
}
```


The following example shows how to run a function as data changes in Azure Cosmos DB.

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

In the *run.ps1* file, you have access to the document that triggers the function via the `$Documents`

parameter.

```
param($Documents, $TriggerMetadata)
Write-Host "First document Id modified : $($Documents[0].id)"
```


The following example shows an Azure Cosmos DB trigger binding. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="CosmosDBTrigger")
@app.cosmos_db_trigger(arg_name="documents",
connection="CONNECTION_SETTING",
database_name="DB_NAME",
container_name="CONTAINER_NAME",
lease_container_name="leases",
create_lease_container_if_not_exists="true")
def test_function(documents: func.DocumentList) -> str:
if documents:
logging.info('Document id: %s', documents[0]['id'])
```


The function writes log messages when Azure Cosmos DB records are modified. Here's the binding data in the *function.json* file:

```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseCollectionName": "leases",
"connectionStringSetting": "<connection-app-setting>",
"databaseName": "Tasks",
"collectionName": "Items",
"createLeaseCollectionIfNotExists": true
}
```


```
{
"type": "cosmosDBTrigger",
"name": "documents",
"direction": "in",
"leaseContainerName": "leases",
"connection": "<connection-app-setting>",
"databaseName": "Tasks",
"containerName": "Items",
"createLeaseContainerIfNotExists": true
}
```


Note that some of the binding attribute names changed in version 4.x of the Azure Cosmos DB extension.

Here's the Python code:

```
import logging
import azure.functions as func
def main(documents: func.DocumentList) -> str:
if documents:
logging.info('First document Id modified: %s', documents[0]['id'])
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated process](dotnet-isolated-process-guide) C# libraries use `CosmosDBTriggerAttribute`

to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-trigger).

The specific properties depends both on the process model and the extension version:

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

In-process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.WebJobs`

namespace, which defines these properties:

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:

| Attribute property |
Description |
**Connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**ContainerName** |
The name of the container being monitored. |
**LeaseConnection** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**CreateLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**LeasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**StartFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

Isolated worker process libraries use [CosmosDBTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.CosmosDB/src/CosmosDBTriggerAttribute.cs) from the `Microsoft.Azure.Functions.Worker`

namespace, which defines these properties:.

| Attribute property |
Description |
**ConnectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**DatabaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**CollectionName** |
The name of the collection being monitored. |
**LeaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `ConnectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**LeaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**LeaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**CreateLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**LeasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `CreateLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**LeaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**FeedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**LeaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**LeaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**LeaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**CheckpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**CheckpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**MaxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**StartFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**PreferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**UseMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |
**UseDefaultJsonSerialization** |
(Optional) Lets you use `JsonConvert.DefaultSettings` in the monitored collection. This setting only applies to the monitored collection and the consumer to setup the serialization used in the monitored collection. The `JsonConvert.DefaultSettings` must be set in a class derived from `CosmosDBWebJobsStartup` . |

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_trigger`

:

| Property |
Description |
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`connection` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

Use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:

| Attribute property |
Description |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**name** |
The name of the function. |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `Connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers isn't [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#nondata-operations-arent-allowed) and your function app isn't allowed to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `CreateLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease isn't renewed within this interval, it expires and ownership of the partition moves to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renewal interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, `East US,South Central US,North Europe` . |

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBTrigger`

annotation on parameters that read data from Azure Cosmos DB. The annotation supports the following properties:


## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.cosmosDB()`

method. The `type`

, `direction`

, and `name`

properties don't apply to the v4 model.

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connection** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](functions-bindings-cosmosdb-v2-trigger#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the container being monitored. |
**containerName** |
The name of the container being monitored. |
**leaseConnection** |
(Optional) The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account that holds the lease container.
When not set, the `connection` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases container must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the container used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseContainerName** |
(Optional) The name of the container used to store leases. When not set, the value `leases` is used. |
**createLeaseContainerIfNotExists** |
(Optional) When set to `true` , the leases container is automatically created when it doesn't already exist. The default value is `false` . When using Microsoft Entra identities if you set the value to `true` , creating containers is not [an allowed operation](/en-us/azure/cosmos-db/troubleshoot-forbidden#non-data-operations-are-not-allowed) and your Function won't be able to start. |
**leasesContainerThroughput** |
(Optional) Defines the number of Request Units to assign when the leases container is created. This setting is only used when `createLeaseContainerIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseContainerPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease container for this function. Using a prefix allows two separate Azure Functions to share the same Lease container by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored container are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the container's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**startFromTime** |
(Optional) Gets or sets the date and time from which to initialize the change feed read operation. The recommended format is ISO 8601 with the UTC designator, such as `2021-02-16T14:19:29Z` . This is only used to set the initial trigger state. After the trigger has a lease state, changing this value has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |

| function.json property |
Description |
**type** |
Must be set to `cosmosDBTrigger` . |
**direction** |
Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
**name** |
The variable name used in function code that represents the list of documents with changes. |
**connectionStringSetting** |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see [Connections](#connections). |
**databaseName** |
The name of the Azure Cosmos DB database with the collection being monitored. |
**collectionName** |
The name of the collection being monitored. |
**leaseConnectionStringSetting** |
(Optional) The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account that holds the lease collection.
When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
**leaseDatabaseName** |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. |
**leaseCollectionName** |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
**createLeaseCollectionIfNotExists** |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
**leasesCollectionThroughput** |
(Optional) Defines the number of Request Units to assign when the leases collection is created. This setting is only used when `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
**leaseCollectionPrefix** |
(Optional) When set, the value is added as a prefix to the leases created in the Lease collection for this function. Using a prefix allows two separate Azure Functions to share the same Lease collection by using different prefixes. |
**feedPollDelay** |
(Optional) The time (in milliseconds) for the delay between polling a partition for new changes on the feed, after all current changes are drained. Default is 5,000 milliseconds, or 5 seconds. |
**leaseAcquireInterval** |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
**leaseExpirationInterval** |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
**leaseRenewInterval** |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
**checkpointInterval** |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
**checkpointDocumentCount** |
(Optional) Customizes the amount of documents between lease checkpoints. Default is after every function call. |
**maxItemsPerInvocation** |
(Optional) When set, this property sets the maximum number of items received per Function call. If operations in the monitored collection are performed through stored procedures, [transaction scope](/en-us/azure/cosmos-db/stored-procedures-triggers-udfs#transactions) is preserved when reading items from the change feed. As a result, the number of items received could be higher than the specified value so that the items changed by the same transaction are returned as part of one atomic batch. |
**startFromBeginning** |
(Optional) This option tells the Trigger to read changes from the beginning of the collection's change history instead of starting at the current time. Reading from the beginning only works the first time the trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this option to `true` when there are leases already created has no effect. |
**preferredLocations** |
(Optional) Defines preferred locations (regions) for geo-replicated database accounts in the Azure Cosmos DB service. Values should be comma-separated. For example, "East US,South Central US,North Europe". |
**useMultipleWriteLocations** |
(Optional) Enables multi-region accounts for writing to the leases collection. |

See the [Example section](#example) for complete examples.

## Usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Attributes section](#attributes).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Annotations section](#annotations).

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `leaseCollectionPrefix`

for each function. Otherwise, only one of the functions is triggered. For information about the prefix, see the [Configuration section](#configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

The parameter type supported by the Azure Cosmos DB trigger depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
| JSON serializable types |
Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type |
Description |
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property |
Environment variable template |
Description |
Example value |
| Account Endpoint |
`<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. |
https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Next steps

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-concurrency -->

# Concurrency in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a single function app instance allows for multiple events to be processed concurrently. Because these run on the same compute instance, they share memory, CPU, and connection resources. In certain hosting plans, high demand on a specific instance causes the Functions host to automatically create new instances to handle the increased load. In these *dynamic scale* plans, there's a tradeoff between concurrency and scaling behaviors. To provide more control over how your app runs, Functions provides a way for you to manage the number of concurrent executions.

Functions provides two main ways of managing concurrency:

[Fixed per-instance concurrency](#fixed-per-instance-concurrency): You can configure host-level limits on concurrency that are specific to individual triggers. This model is the default concurrency behavior for Functions.[Dynamic concurrency](#dynamic-concurrency): For certain trigger types, the Functions host can automatically determine the best level of concurrency for that trigger in your function app. You must[opt in to this concurrency model](#dynamic-concurrency-configuration).

This article describes the concurrency behaviors of event-driven triggers in Functions and how these behaviors affect scaling in dynamic plans. It also compares the fixed per-instance and dynamic concurrency models.

## Scaling versus concurrency

For functions that use event-based triggers or respond to HTTP requests, you can quickly reach the limits of concurrent executions during periods of high demand. During such periods, you must be able to scale your function app by adding instances to avoid a backlog in processing incoming requests. The way that we scale your app depends on your hosting plan:

| Scale type | Hosting plans | Description |
|---|---|---|
| Dynamic (event-driven) scaling |
|

[Event-driven scaling in Azure Functions](event-driven-scaling).[Dedicated (App Service) plans](dedicated-plan)[set up an autoscale scheme](dedicated-plan#scaling).Before any scaling might occur, your function app attempts to handle increases in load by handling multiple invocations of the same type in a single instance. As a result, these concurrent executions on a given instance directly impact scale decisions. For instance, when an app in a dynamic scale plan hits a concurrency limit, it might need to scale to keep up with incoming demand.

The balance of scale versus concurrency you try to achieve in your app depends on where bottlenecks might occur: in processing (CPU-intensive process limitations) or in a downstream service (I/O-based limitations).

## Fixed per-instance concurrency

By default, most triggers support a fixed per-instance concurrency configuration model via [target-based scaling](functions-target-based-scaling). In this model, each trigger type has a per-instance concurrency limit.

You can override the concurrency default values for most triggers by setting a specific per-instance concurrency for that trigger type. For many triggers, you configure concurrency settings in the [host.json file](functions-host-json). For example, the [Azure Service Bus trigger](functions-bindings-service-bus-trigger) provides both a `MaxConcurrentCalls`

and a `MaxConcurrentSessions`

setting in *host.json*. These settings work together to control the maximum number of messages that each function app processes concurrently on each instance.

In certain target-based scaling scenarios, such as when you use an Apache Kafka or Azure Cosmos DB trigger, the concurrency configuration is in the function declaration, not in the *host.json* file. Other trigger types have built-in mechanisms for load balancing invocations across instances. For example, Azure Event Hubs and Azure Cosmos DB both use a partition-based scheme.

For trigger types that support concurrency configuration, the concurrency settings are applied to all running instances. This way, you can control the maximum concurrency for your functions on each instance. For example, when your function is CPU-intensive or resource-intensive, you might choose to limit concurrency to keep instances healthy. In this case, you can rely on scaling to handle increased loads. Similarly, when your function makes requests to a downstream service that's being throttled, you should also consider limiting concurrency to avoid overloading the downstream service.

## HTTP trigger concurrency

*Applies only to the Flex Consumption plan*

HTTP trigger concurrency is a special type of fixed per-instance concurrency. In HTTP trigger concurrency, the default concurrency also depends on the [instance size](flex-consumption-plan#instance-sizes).

The Flex Consumption plan scales all HTTP trigger functions together as a group. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling).

The following table indicates the default concurrency setting for HTTP triggers on a given instance, based on the configured instance memory size:

| Instance size (MB) | Default concurrency* |
|---|---|
| 512 | 4 |
| 2,048 | 16 |
| 4,096 | 32 |

*In Python apps, all instance sizes use an HTTP trigger concurrency level of one by default.

These default values should work well for most cases, and you can start with them. Consider that at a given number of HTTP requests, increasing the HTTP concurrency value reduces the number of instances required to handle HTTP requests. Likewise, decreasing the HTTP concurrency value requires more instances to handle the same load.

If you need to fine-tune the HTTP concurrency, you can do so by using the Azure CLI. For more information, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits).

The default concurrency values in the preceding table apply only when you don't set your own HTTP concurrency setting. When you don't explicitly set an HTTP concurrency setting, the default concurrency increases as shown in the table when you change the instance size. After you specifically set an HTTP concurrency value, that value is maintained despite changes in the instance size.

## Determine optimal fixed per-instance concurrency

Fixed per-instance concurrency configurations give you control of certain trigger behaviors, such as throttling your functions. But it can be difficult to determine the optimal values for these settings. Generally, you have to arrive at acceptable values by an iterative process of load testing. Even after you determine a set of values that work for a particular load profile, the number of events that arrive from your connected services can change from day to day. This variability can cause your app to run with suboptimal values. For example, your function app might process demanding message payloads on the last day of the week, which requires you to throttle concurrency down. However, during the rest of the week, the message payloads might be lighter, which means you can use a higher concurrency level the rest of the week.

Ideally, the system should allow instances to process as much work as they can while keeping each instance healthy and latencies low. Dynamic concurrency is designed for that purpose.

## Dynamic concurrency

Functions provides a dynamic concurrency model that simplifies configuring concurrency for all function apps that run in the same plan.

Note

Dynamic concurrency is currently only supported for the Azure Blob Storage, Azure Queue Storage, and Service Bus triggers. Also, you must use the extension versions listed in [Extension support](#extension-support), later in this article.

### Benefits

Dynamic concurrency provides the following benefits:

**Simplified configuration**: You no longer have to manually determine per-trigger concurrency settings. The system learns the optimal values for your workload over time.**Dynamic adjustments**: Concurrency is adjusted up or down dynamically in real time, which allows the system to adapt to changing load patterns over time.**Instance health protection**: The runtime limits concurrency to levels that a function app instance can comfortably handle. These limits protect the app from overloading itself by taking on more work than it should.**Improved throughput**: Overall throughput is improved, because individual instances don't pull more work than they can quickly process. As a result, work is load-balanced more effectively across instances. For functions that can handle higher loads, higher throughput can be obtained by increasing concurrency to values above the default configuration.

### Dynamic concurrency configuration

You can turn on dynamic concurrency at the host level in the *host.json* file. When it's turned on, the concurrency levels of any binding extensions that support this feature are adjusted automatically as needed. In these cases, dynamic concurrency settings override any manually configured concurrency settings.

By default, dynamic concurrency is turned off. When you turn on dynamic concurrency, concurrency starts at a level of one for each function. The concurrency level is adjusted up to an optimal value, which the host determines.

You can turn on dynamic concurrency in your function app by adding the following settings to your *host.json* file:

```
{
"version": "2.0",
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


When `snapshotPersistenceEnabled`

is `true`

, which is the default value, the learned concurrency values are periodically persisted to storage. New instances start from those values instead of starting from a level of one and having to redo the learning.

### Concurrency manager

Behind the scenes, when dynamic concurrency is turned on, a concurrency manager process runs in the background. This manager constantly monitors instance health metrics, like CPU and thread utilization, and changes throttles as needed. When one or more throttles are turned on, function concurrency is adjusted down until the host is healthy again. When throttles are turned off, concurrency can increase. Various heuristics are used to intelligently adjust concurrency up or down as needed based on these throttles. Over time, concurrency for each function stabilizes to a particular level. Because it can take time to determine the optimal concurrency value, use dynamic concurrency only if a suboptimal value is acceptable for your solution initially or after a period of inactivity.

Concurrency levels are managed for each individual function. Specifically, the system balances between resource-intensive functions that require a low level of concurrency and more lightweight functions that can handle higher concurrency. The balance of concurrency for each function helps to maintain the overall health of the function app instance.

When dynamic concurrency is turned on, you find dynamic concurrency decisions in your logs. For example, log entries are added when various throttles are turned on, and whenever concurrency is adjusted up or down for each function. These logs are written under the **Host.Concurrency** log category in the **traces** table.

### Extension support

Dynamic concurrency is enabled for a function app at the host level, and any extensions that support dynamic concurrency run in that mode. Dynamic concurrency requires collaboration between the host and individual trigger extensions. Only the listed versions of the following extensions support dynamic concurrency.

| Extension | Version | Description |
|---|---|---|
Queue Storage |
|

`BatchSize`

and `NewBatchThreshold`

configuration options govern concurrency. When you use dynamic concurrency, those configuration values are ignored. Dynamic concurrency is integrated into the message loop, so the number of messages retrieved per iteration is dynamically adjusted. When throttles are turned on, the host is overloaded. Message processing is paused until the throttles are turned off. When the throttles are turned off, concurrency increases.**Blob Storage**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage)(Storage extension)**Service Bus**[Version 5.x](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)**Single dispatch topic/queue processing**: Each invocation of your function processes a single message. When you use a fixed per-instance configuration, the

`MaxConcurrentCalls`

configuration option governs concurrency. When you use dynamic concurrency, that configuration value is ignored, and concurrency is adjusted dynamically.**Session-based single dispatch topic/queue processing**: Each invocation of your function processes a single message. Depending on the number of active sessions for your topic or queue, each instance leases one or more sessions. Messages in each session are processed serially, to guarantee ordering in a session. When you don't use dynamic concurrency, the

`MaxConcurrentSessions`

setting governs concurrency. When dynamic concurrency is turned on, the `MaxConcurrentSessions`

value is ignored, and the number of sessions that each instance processes is dynamically adjusted.**Batch processing**: Each invocation of your function processes a batch of messages, governed by the

`MaxMessageCount`

setting. Because batch invocations are serial, concurrency for your batch-triggered function is always one, and dynamic concurrency doesn't apply.## Next steps

For more information, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/run-functions-from-deployment-package -->

# Run your functions from a package file in Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure, you can run your functions directly from a deployment package file in your function app. The other option is to deploy your files in the `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux) directory of your function app.

This article describes the benefits of running your functions from a package. It also shows how to enable this functionality in your function app.

## Benefits of running from a package file

There are several benefits to running functions from a package file:

- Reduces the risk of file copy locking issues.
- Can be deployed to a production app (with restart).
- Verifies the files that are running in your app.
- Improves the performance of
[Azure Resource Manager deployments](functions-infrastructure-as-code). - Reduces cold-start times, particularly for JavaScript functions with large npm package trees.

For more information, see [this announcement](https://github.com/Azure/app-service-announcements/issues/84).

## Enable functions to run from a package

Function apps on the [Flex Consumption](flex-consumption-plan) hosting plan run from a package by default. No special configuration needs to be done.

To enable your function app to run from a package on the [Consumption](consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) hosting plans, add a `WEBSITE_RUN_FROM_PACKAGE`

app setting to your function app. The `WEBSITE_RUN_FROM_PACKAGE`

app setting can have one of the following values:

| Value | Description |
|---|---|
`1` |
Indicates that the function app runs from a local package file deployed in the `c:\home\data\SitePackages` (Windows) or `/home/data/SitePackages` (Linux) folder of your function app. This is the default option when you use
|
`<URL>` |
Sets a URL that is the remote location of the specific package file you want to run. Required for functions apps running on Linux in a Consumption plan. |

The following table indicates the recommended `WEBSITE_RUN_FROM_PACKAGE`

values for deployment to a specific operating system and hosting plan:

| Hosting plan | Windows | Linux |
|---|---|---|
|

`1`

is highly recommended.`<URL>`

is supported.[Premium](functions-premium-plan)`1`

is recommended.`1`

is recommended.[Dedicated](dedicated-plan)`1`

is recommended.`1`

is recommended.## General considerations

- Do not add the
`WEBSITE_RUN_FROM_PACKAGE`

app setting to apps on the[Flex Consumption](flex-consumption-plan)plan. - The package file must be .zip formatted. Tar and gzip formats aren't supported.
[Zip deployment](#integration-with-zip-deployment)is recommended.- When deploying your function app to Windows, you should set
`WEBSITE_RUN_FROM_PACKAGE`

to`1`

and publish with zip deployment. - When you run from a package, the
`wwwroot`

folder is read-only and you receive an error if you write files to this directory. Files are also read-only in the Azure portal. - The maximum size for a deployment package file is 1 GB.
- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
[500 MB per plan](functions-scale#service-limits). To learn about how to troubleshoot issues with temporary storage, see[How to troubleshoot temporary storage on Azure App Service](/en-us/troubleshoot/azure/app-service/temporary-storage-for-azure-app-service).

- The deployment uses temporary storage when unpacking your project files. This means that your function app must have enough available temporary storage space to hold the contents of your package. Keep in mind that the temporary storage limit for a Consumption plan is
- You can't use the local cache when running from a deployment package.
- If your project needs to use remote build, don't use the
`WEBSITE_RUN_FROM_PACKAGE`

app setting. Instead, add the`SCM_DO_BUILD_DURING_DEPLOYMENT=true`

deployment customization app setting. For Linux, also add the`ENABLE_ORYX_BUILD=true`

setting. For more information, see[Remote build](functions-deployment-technologies#remote-build).

Note

The `WEBSITE_RUN_FROM_PACKAGE`

app setting does not work with MSDeploy as described in [MSDeploy VS. ZipDeploy](https://github.com/projectkudu/kudu/wiki/MSDeploy-VS.-ZipDeploy). You will receive an error during deployment, such as `ARM-MSDeploy Deploy Failed`

. To resolve this error, change `/MSDeploy`

to `/ZipDeploy`

.

### Add the WEBSITE_RUN_FROM_PACKAGE setting

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Creating the zip archive

The zip archive you deploy must contain all of the files needed to run your function app. You can manually create a zip archive from the contents of a Functions project folder using built-in .zip compression functionality or non-Microsoft tools.

The archive must include the [host.json](functions-host-json) file at the root of the extracted folder. The selected language stack for the function app creates other requirements:

Important

For languages that generate compiled output for deployment, make sure to compress the contents of the output folder you plan to publish and not the entire project folder. When Functions extracts the contents of the zip archive, the `host.json`

file must exist in the root of the package.

## Use WEBSITE_RUN_FROM_PACKAGE = 1

This section provides information about how to run your function app from a local package file.

### Considerations for deploying from an on-site package

- Using an on-site package is the recommended option for running from the deployment package, except when running on Linux hosted in a Consumption plan.
[Zip deployment](#integration-with-zip-deployment)is the recommended way to upload a deployment package to your site.- When not using zip deployment, make sure the
`c:\home\data\SitePackages`

(Windows) or`/home/data/SitePackages`

(Linux) folder has a file named`packagename.txt`

. This file contains only the name, without any whitespace, of the package file in this folder that's currently running.

### Integration with zip deployment

Zip deployment is a feature of Azure App Service that lets you deploy your function app project to the `wwwroot`

directory. The project is packaged as a .zip deployment file. The same APIs can be used to deploy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder.

When you set the `WEBSITE_RUN_FROM_PACKAGE`

app setting value to `1`

, the zip deployment APIs copy your package to the `c:\home\data\SitePackages`

(Windows) or `/home/data/SitePackages`

(Linux) folder instead of extracting the files to `c:\home\site\wwwroot`

(Windows) or `/home/site/wwwroot`

(Linux). It also creates the `packagename.txt`

file. After your function app is automatically restarted, the package is mounted to `wwwroot`

as a read-only filesystem. For more information about zip deployment, see [Zip deployment for Azure Functions](deployment-zip-push).

Note

When a deployment occurs, a restart of the function app is triggered. Function executions currently running during the deploy are terminated. For information about how to write stateless and defensive functions, sett [Write functions to be stateless](performance-reliability#write-functions-to-be-stateless).

## Use WEBSITE_RUN_FROM_PACKAGE = URL

This section provides information about how to run your function app from a package deployed to a URL endpoint. This option is the only one supported for running from a Linux-hosted package with a Consumption plan. This option is not supported in the [Flex Consumption](flex-consumption-plan) plan.

### Considerations for deploying from a URL

- Do not set
`WEBSITE_RUN_FROM_PACKAGE = <URL>`

in apps on the[Flex Consumption](flex-consumption-plan)plan. This option is not supported. - Function apps running on Windows experience a slight increase in
[cold-start time](event-driven-scaling#cold-start)when the application package is deployed to a URL endpoint via`WEBSITE_RUN_FROM_PACKAGE = <URL>`

. - When you specify a URL, you must also
[manually sync triggers](functions-deployment-technologies#trigger-syncing)after you publish an updated package. - The Functions runtime must have permissions to access the package URL.
- Don't deploy your package to Azure Blob Storage as a public blob. Instead, use a private container with a
[shared access signature (SAS)](../storage/common/storage-sas-overview)or[use a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity)to enable the Functions runtime to access the package. - You must maintain any SAS URLs used for deployment. When an SAS expires, the package can no longer be deployed. In this case, you must generate a new SAS and update the setting in your function app. You can eliminate this management burden by
[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity). - When running on a Premium plan, make sure to
[eliminate cold starts](functions-premium-plan#eliminate-cold-starts). - When you're running on a Dedicated plan, ensure you enable
[Always On](dedicated-plan#always-on). - You can use
[Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer)to upload package files to blob containers in your storage account.

### Manually uploading a package to Blob Storage

To deploy a zipped package when using the URL option, you must create a .zip compressed deployment package and upload it to the destination. The following procedure deploys to a container in Blob Storage:

Create a .zip package for your project using the utility of your choice.

In the

[Azure portal](https://portal.azure.com), search for your storage account name or browse for it in the storage accounts list.In the storage account, select

**Containers**under**Data storage**.Select

**+ Container**to create a new Blob Storage container in your account.In the

**New container**page, provide a**Name**(for example,*deployments*), ensure the**Anonymous access level**is**Private**, and then select**Create**.Select the container you created, select

**Upload**, browse to the location of the .zip file you created with your project, and then select**Upload**.After the upload completes, choose your uploaded blob file, and copy the URL. If you aren't

[using a managed identity](#fetch-a-package-from-azure-blob-storage-using-a-managed-identity), you might need to generate a SAS URL.Search for your function app or browse for it in the

**Function App**page.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**+ Add**.Enter the value

`WEBSITE_RUN_FROM_PACKAGE`

for the**Name**, and paste the URL of your package in Blob Storage for the**Value**.Select

**Apply**, and then select**Apply**and**Confirm**to save the setting and restart the function app.

Now you can run your function in Azure to verify that deployment of the deployment package .zip file was successful.

### Fetch a package from Azure Blob Storage using a managed identity

You can configure Azure Blob Storage to [authorize requests with Microsoft Entra ID](/en-us/azure/storage/blobs/authorize-access-azure-active-directory?toc=%2fazure%2fstorage%2fblobs%2ftoc.json). This configuration means that instead of generating a SAS key with an expiration, you can instead rely on the application's [managed identity](/en-us/azure/app-service/overview-managed-identity). By default, the app's system-assigned identity is used. If you wish to specify a user-assigned identity, you can set the `WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept `SystemAssigned`

as a value, which is equivalent to omitting the setting.

To enable the package to be fetched using the identity:

Ensure that the blob is

[configured for private access](/en-us/azure/storage/blobs/anonymous-read-access-configure#set-the-anonymous-access-level-for-a-container).Grant the identity the

[Storage Blob Data Reader](/en-us/azure/role-based-access-control/built-in-roles#storage-blob-data-reader)role with scope over the package blob. See[Assign an Azure role for access to blob data](/en-us/azure/storage/blobs/assign-azure-role-data-access)for details on creating the role assignment.Set the

`WEBSITE_RUN_FROM_PACKAGE`

application setting to the blob URL of the package. This URL is usually of the form`https://{storage-account-name}.blob.core.windows.net/{container-name}/{path-to-package}`

or similar.If you wish to specify a user-assigned identity, you can set the

`WEBSITE_RUN_FROM_PACKAGE_BLOB_MI_RESOURCE_ID`

app setting to the resource ID of that identity. The setting can also accept "SystemAssigned" as a value, although this is the same as omitting the setting altogether. A resource ID is a standard representation for a resource in Azure. For a user-assigned managed identity, that is going to be`/subscriptions/subid/resourcegroups/rg-name/providers/Microsoft.ManagedIdentity/userAssignedIdentities/identity-name`

. The resource ID of a user-assigned managed identity can be obtained in the**Settings**->**Properties**->**ID for the user assigned managed identity**.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/self-hosted-mcp-servers -->

# Self-hosted remote MCP server on Azure Functions (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides two ways of hosting remote MCP servers:

- MCP servers created with the
[Functions MCP extension](functions-bindings-mcp) - MCP servers built with the
[official MCP SDKs](https://modelcontextprotocol.io/docs/sdk)

With the first approach, you can use the Azure Functions programming model with triggers and bindings to build the MCP server. Then, you can host the server remotely by deploying it to a Function app.

If you already have an MCP server created with the official MCP SDKs and just want to host it remotely, the second approach likely suits your needs. You don't need to make any code changes to the server to host it on Azure Functions. Instead, you can add the required Functions artifacts, and the server is ready to be deployed. As such, these servers are referred to as *self-hosted MCP servers*.


This article provides an overview of self-hosted MCP servers and links to relevant articles and samples.

## Custom handlers

Self-hosted MCP servers deploy to the Azure Functions platform as *custom handlers*. Custom handlers are lightweight web servers that receive events from the Functions host. They provide a way to run on the Functions platform applications built with frameworks different from the Functions programming model or in languages not supported out-of-the-box. For more information, see [Azure Functions custom handlers](functions-custom-handlers).

When you deploy an MCP SDK based server to Azure Functions, you must include a *host.json* in your project. The minimal *host.json* looks like this:

```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "python",
"arguments": ["Path to main script file, e.g. hello_world.py"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "npm",
"arguments": ["run", "start"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "dotnet",
"arguments": ["Path to the compiled DLL, e.g. HelloWorld.dll"]
},
"port": "<MCP server port>"
}
}
```


Note

Because the payload deployed to Azure Functions is the content of the `bin/output`

directory, the path to the compiled DLL is relative to that directory, *not* to the project root.

Example not yet available.

Using a `configuration Profile`

value of `mcp-custom-handler`

automatically configures these Functions host settings, which are required for running your MCP server in Azure Functions:

`http.enableProxying`

to`true`

`http.routes`

to`[{ "route": "{*route}" }]`

`extensions.http.routePrefix`

to`""`


This example shows a host.json file with extra custom handler properties set equivalent to using the `mcp-custom-handler`

profile:

```
{
"version": "2.0",
"extensions": {
"http": {
"routePrefix": ""
}
},
"customHandler": {
"description": {
"defaultExecutablePath": "",
"arguments": [""]
},
"http": {
"enableProxying": true,
"defaultAuthorizationLevel": "anonymous",
"routes": [
{
"route": "{*route}",
// Default authorization level is `defaultAuthorizationLevel`
},
{
"route": "admin/{*route}",
"authorizationLevel": "admin"
}
]
}
}
}
```


This table explains the properties of `customHandler.http`

, along with default values:

| Property | What it does | Default value |
|---|---|---|
`enableProxying` |
Controls how the Azure Functions host handles HTTP requests to custom handlers. When `enableProxying` is set to `true` , the Functions host acts as a reverse proxy and forwards the entire HTTP request (including headers, body, query parameters) directly to the custom handler. This setting gives the custom handler full access to the original HTTP request details. When `enableProxying` is `false` , the Functions host processes the request first and transforms it into the Azure Functions request/response format before passing it to the custom handler. |
`false` |
`defaultAuthorizationLevel` |
Controls the authentication requirement for accessing custom handler endpoints. For example, `function` requires a function-specific API key to access. For more information, see
|
`function` |
`route` |
Specifies the URL path pattern that the custom handler responds to. `{*route}` matches any URL path (such as `/` , `/mcp` , `/api/tools` , or `/anything/nested/path` ) and forwards the request to the custom handler. |
`{*route}` |

## Built-in server authentication

OAuth-based authentication and authorization provided by the App Service platform implements the requirements of the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), such as issuing 401 challenge and exposing the Protected Resource Metadata (PRM) document. When you enable built-in authentication, clients attempting to access the server are redirected to identity providers like Microsoft Entra ID for authentication before connecting.

For more information, see [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) and [Hosting MCP servers on Azure Functions](functions-mcp-tutorial).

## Azure AI Foundry agent integrations

Agents in Azure AI Foundry can be [configured to use tools](functions-mcp-tutorial#configure-azure-ai-foundry-agent-to-use-your-tools) in MCP servers hosted in Azure Functions.

## Register your server in Azure API Center

When you register your MCP server in Azure API Center, you create a private organizational tool catalog. This approach is recommended for sharing MCP servers across your organization with consistent governance and discoverability. For more information, see [Register MCP servers hosted in Azure Functions in Azure API Center](register-mcp-server-api-center).

## Public preview support

The ability to host your own SDK-based MCP servers in Functions is currently in preview and supports these features:

**Stateless**servers that use the**streamable-http**transport. If you need your server to be stateful, consider using the Functions MCP extension.- Servers implemented with the Python, TypeScript, C#, or Java MCP SDKs.
- When running the project locally, you must use the Azure Functions Core Tools (
`func start`

command). You can't currently use`F5`

to start running with the debugger. - Servers must be hosted as
[Flex Consumption plan](flex-consumption-plan)apps.

## Samples

Not yet available.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-warmup -->

# Azure Functions warmup trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with the warmup trigger in Azure Functions. A warmup trigger is invoked when an instance is added to scale a running function app. The warmup trigger lets you define a function that runs when a new instance of your function app is started. You can use a warmup trigger to preload custom dependencies so your functions are ready to start processing requests immediately. Some actions for a warmup trigger might include opening connections, loading dependencies, or running any other custom logic before your app begins receiving traffic.

The following considerations apply when using a warmup trigger:

- There can be only one warmup trigger function per function app, and it can't be invoked after the instance is already running.
- The name of the function that is the warmup trigger for your app should be
`warmup`

(case-insensitive). - The warmup trigger isn't available to apps running on the
[Consumption plan](consumption-plan). - The warmup trigger isn't supported on version 1.x of the Functions runtime.
- Support for the warmup trigger is provided by default in all development environments. You don't have to manually install the package or register the extension.
- The warmup trigger is only called during scale-out operations, not during restarts or other nonscaling startups. Make sure your logic can load all required dependencies without relying on the warmup trigger. Lazy loading is a good pattern to achieve this goal.
- Dependencies created by warmup trigger should be shared with other functions in your app. To learn more, see
[Static clients](manage-connections#static-clients). - If the
[built-in authentication](../app-service/overview-authentication-authorization)(also known as Easy Auth) is used,[HTTPS Only](../app-service/configure-ssl-bindings#enforce-https)should be enabled for the warmup trigger to get invoked.

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that runs on each new instance when added to your app.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class Warmup
{
[Function(nameof(Warmup))]
public static void Run([WarmupTrigger] object warmupContext, FunctionContext context)
{
var logger = context.GetLogger(nameof(Warmup));
logger.LogInformation("Function App instance is now warm!");
}
}
}
```


The following example shows a warmup trigger that runs when each new instance is added to your app.

```
@FunctionName("Warmup")
public void warmup( @WarmupTrigger Object warmupContext, ExecutionContext context) {
context.getLogger().info("Function App instance is warm.");
}
```


The following example shows a [JavaScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
const { app } = require('@azure/functions');
app.warmup('warmupTrigger', {
handler: (warmupContext, context) => {
context.log('Function App instance is warm.');
},
});
```


The following example shows a [TypeScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
import { app, InvocationContext, WarmupContext } from '@azure/functions';
export async function warmupFunction(warmupContext: WarmupContext, context: InvocationContext): Promise<void> {
context.log('Function App instance is warm.');
}
app.warmup('warmup', {
handler: warmupFunction,
});
```


Here's the *function.json* file:

```
{
"bindings": [
{
"type": "warmupTrigger",
"direction": "in",
"name": "warmupContext"
}
]
}
```


PowerShell example code pending.

The following example shows a warmup trigger in a *function.json* file and a [Python function](functions-reference-python) that runs on each new instance when it'is added to your app.

Your function must be named `warmup`

(case-insensitive) and there can only be one warmup function per app.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.warm_up_trigger('warmup')
def warmup(warmup) -> None:
logging.info('Function App instance is warm')
```


For more information, see [Configuration](#configuration).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `WarmupTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

Use the `WarmupTrigger`

attribute to define the function. This attribute has no parameters.

## Annotations

Warmup triggers don't require annotations. Just use a name of `warmup`

(case-insensitive) for the `FunctionName`

annotation.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required - must be set to `warmupTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code. A `name` of `warmupContext` is recommended for the binding parameter. |

See the [Example section](#example) for complete examples.

## Usage

The following considerations apply to using a warmup function in C#:

- Your function must be named
`warmup`

(case-insensitive) using the`Function`

attribute. - A return value attribute isn't required.
- Use the
`Microsoft.Azure.Functions.Worker.Extensions.Warmup`

package - You can pass an object instance to the function.

Your function must be named `warmup`

(case-insensitive) using the `FunctionName`

annotation.

The function type in function.json must be set to `warmupTrigger`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-output -->

# SignalR Service output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the *SignalR* output binding to send one or more messages using Azure SignalR Service. You can broadcast a message to:

- All connected clients
- Connected clients in a specified group
- Connected clients authenticated to a specific user

The output binding also allows you to manage groups, such as adding a client or user to a group, removing a client or user from a group.

For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

### Broadcast to all clients

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a function that sends a message using the output binding to all connected clients. The *newMessage* is the name of the method to be invoked on each client.

```
[Function(nameof(BroadcastToAll))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction BroadcastToAll([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
// broadcast to all the connected clients without specifying any connection, user or group.
Arguments = new[] { bodyReader.ReadToEnd() },
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
// You can use any other trigger type instead.
app.http('broadcast', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body]
});
}
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


### Send to a user

You can send a message only to connections that have been authenticated to a user by setting the *user ID* in the SignalR message.

```
[Function(nameof(SendToUser))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction SendToUser([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
Arguments = new[] { bodyReader.ReadToEnd() },
UserId = "userToSend",
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
#message will only be sent to this user ID
'userId': 'userId1',
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.userId = "userId1";
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.http('sendToUser', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body],
"userId": "userId1",
});
}
});
```


### Send to a group

You can send a message only to connections that have been added to a group by setting the *group name* in the SignalR message.

```
[Function(nameof(SendToGroup))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRMessageAction SendToGroup([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
using var bodyReader = new StreamReader(req.Body);
return new SignalRMessageAction("newMessage")
{
Arguments = new[] { bodyReader.ReadToEnd() },
GroupName = "groupToSend"
};
}
```


Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.http('sendToGroup', {
methods: ['GET'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"target": "newMessage",
"arguments": [request.body],
"groupName": "myGroup",
});
}
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
message = req.get_json()
signalROutput.set(json.dumps({
#message will only be sent to this group
'groupName': 'myGroup',
'target': 'newMessage',
'arguments': [ message ]
}))
```


```
@FunctionName("sendMessage")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRMessage sendMessage(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req) {
SignalRMessage message = new SignalRMessage();
message.groupName = "myGroup";
message.target = "newMessage";
message.arguments.add(req.getBody());
return message;
}
```


### Group management

SignalR Service allows users or connections to be added to groups. Messages can then be sent to a group. You can use the `SignalR`

output binding to manage groups.

Specify `SignalRGroupActionType`

to add or remove a member. The following example removes a user from a group.

```
[Function(nameof(RemoveFromGroup))]
[SignalROutput(HubName = "chat", ConnectionStringSetting = "SignalRConnection")]
public static SignalRGroupAction RemoveFromGroup([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req)
{
return new SignalRGroupAction(SignalRGroupActionType.Remove)
{
GroupName = "group1",
UserId = "user1"
};
}
```


Note

In order to get the `ClaimsPrincipal`

correctly bound, you must have configured the authentication settings in Azure Functions.

Here's binding data in the *function.json* file:

Example function.json:

```
{
"type": "signalR",
"name": "signalROutput",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "out"
}
```


```
const { app, output } = require('@azure/functions');
const signalR = output.generic({
type: 'signalR',
name: 'signalR',
hubName: 'hub',
connectionStringSetting: 'AzureSignalRConnectionString',
});
// The following function adds a user to a group
app.http('addUserToGroup', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"userId": req.query.userId,
"groupName": "myGroup",
"action": "add"
});
}
});
// The following function removes a user from a group
app.http('removeUserFromGroup', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [signalR],
handler: (request, context) => {
context.extraOutputs.set(signalR, {
"userId": req.query.userId,
"groupName": "myGroup",
"action": "remove"
});
}
});
```


Complete PowerShell examples are pending.

The following example adds a user to a group.

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
signalROutput.set(json.dumps({
'userId': 'userId1',
'groupName': 'myGroup',
'action': 'add'
}))
```


The following example removes a user from a group.

```
def main(req: func.HttpRequest, signalROutput: func.Out[str]) -> func.HttpResponse:
signalROutput.set(json.dumps({
'userId': 'userId1',
'groupName': 'myGroup',
'action': 'remove'
}))
```


The following example adds a user to a group.

```
@FunctionName("addToGroup")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRGroupAction addToGroup(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req,
@BindingName("userId") String userId) {
SignalRGroupAction groupAction = new SignalRGroupAction();
groupAction.action = "add";
groupAction.userId = userId;
groupAction.groupName = "myGroup";
return action;
}
```


The following example removes a user from a group.

```
@FunctionName("removeFromGroup")
@SignalROutput(name = "$return", HubName = "hubName1")
public SignalRGroupAction removeFromGroup(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Object> req,
@BindingName("userId") String userId) {
SignalRGroupAction groupAction = new SignalRGroupAction();
groupAction.action = "remove";
groupAction.userId = userId;
groupAction.groupName = "myGroup";
return action;
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

The following table explains the properties of the `SignalROutput`

attribute.

| Attribute property | Description |
|---|---|
HubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Annotations

The following table explains the supported settings for the `SignalROutput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `signalR` . |
direction |
Must be set to `out` . |
name |
Variable name used in function code for connection info object. |
hubName |
This value must be set to the name of the SignalR hub for which the connection information is generated. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-input -->

# Azure Blob storage input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The input binding allows you to read blob storage data as input to an Azure Function.

For information on setup and configuration details, see the [overview](functions-bindings-storage-blob).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example is a [C# function](dotnet-isolated-process-guide) that runs in an isolated worker process and uses a blob trigger with both blob input and blob output blob bindings. The function is triggered by the creation of a blob in the *test-samples-trigger* container. It reads a text file from the *test-samples-input* container and creates a new text file in an output container based on the name of the triggered file.

```
public static class BlobFunction
{
[Function(nameof(BlobFunction))]
[BlobOutput("test-samples-output/{name}-output.txt")]
public static string Run(
[BlobTrigger("test-samples-trigger/{name}")] string myTriggerItem,
[BlobInput("test-samples-input/sample1.txt")] string myBlob,
FunctionContext context)
{
var logger = context.GetLogger("BlobFunction");
logger.LogInformation("Triggered Item = {myTriggerItem}", myTriggerItem);
logger.LogInformation("Input Item = {myBlob}", myBlob);
// Blob Output
return "blob-output content";
}
}
}
```


This section contains the following examples:

[HTTP trigger: look up blob name from query string](#http-trigger-look-up-blob-name-from-query-string)[Queue trigger: receive blob name from queue message](#queue-trigger-receive-blob-name-from-queue-message)

#### HTTP trigger, look up blob name from query string

The following example shows a Java function that uses the `HttpTrigger`

annotation to receive a parameter containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

.

```
@FunctionName("getBlobSizeHttp")
@StorageAccount("Storage_Account_Connection_String")
public HttpResponseMessage blobSize(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{Query.file}")
byte[] content,
final ExecutionContext context) {
// build HTTP response with size of requested blob
return request.createResponseBuilder(HttpStatus.OK)
.body("The size of \"" + request.getQueryParameters().get("file") + "\" is: " + content.length + " bytes")
.build();
}
```


#### Queue trigger: receive blob name from queue message

The following example shows a Java function that uses the `QueueTrigger`

annotation to receive a message containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

.

```
@FunctionName("getBlobSize")
@StorageAccount("Storage_Account_Connection_String")
public void blobSize(
@QueueTrigger(
name = "filename",
queueName = "myqueue-items-sample")
String filename,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{queueTrigger}")
byte[] content,
final ExecutionContext context) {
context.getLogger().info("The size of \"" + filename + "\" is: " + content.length + " bytes");
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@BlobInput`

annotation on parameters whose value would come from a blob. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

This example shows how to get the BlobClient from both a Storage Blob trigger and from the input binding on an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import { app, InvocationContext } from "@azure/functions";
export async function storageBlobTrigger(
blobStorageClient: StorageBlobClient, // SDK binding provides this client
context: InvocationContext
): Promise<void> {
context.log(`Blob trigger processing: ${context.triggerMetadata.name}`);
// Access to full SDK capabilities
const blobProperties = await blobStorageClient.blobClient.getProperties();
context.log(`Blob size: ${blobProperties.contentLength}`);
// Download blob content
const downloadResponse = await blobStorageClient.blobClient.download();
context.log(`Content: ${downloadResponse}`);
}
// Register the function
app.storageBlob("storageBlobTrigger", {
path: "snippets/{name}",
connection: "AzureWebJobsStorage",
sdkBinding: true, // Enable SDK binding
handler: storageBlobTrigger,
});
```


This example shows how to get the `ContainerClient`

from both a Storage Blob input binding using an HTTP trigger:

```
import "@azure/functions-extensions-blob"; // This is the mandatory first import for SDK binding
import { StorageBlobClient } from "@azure/functions-extensions-blob";
import {
app,
HttpRequest,
HttpResponseInit,
input,
InvocationContext,
} from "@azure/functions";
const blobInput = input.storageBlob({
path: "snippets",
connection: "AzureWebJobsStorage",
sdkBinding: true,
});
export async function listBlobs(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
// Get input binding for a specific container
const storageBlobClient = context.extraInputs.get(
blobInput
) as StorageBlobClient;
// List all blobs in the container
const blobs = [];
for await (const blob of storageBlobClient.containerClient.listBlobsFlat()) {
blobs.push(blob.name);
}
return { jsonBody: { blobs } };
}
app.http("listBlobs", {
methods: ["GET"],
authLevel: "function",
extraInputs: [blobInput],
handler: listBlobs,
});
```


The following example shows a queue triggered [TypeScript function](functions-reference-node?tabs=typescript) that makes a copy of a blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

```
import { app, input, InvocationContext, output } from '@azure/functions';
const blobInput = input.storageBlob({
path: 'samples-workitems/{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
const blobOutput = output.storageBlob({
path: 'samples-workitems/{queueTrigger}-Copy',
connection: 'MyStorageConnectionAppSetting',
});
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<unknown> {
return context.extraInputs.get(blobInput);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [blobInput],
return: blobOutput,
handler: storageQueueTrigger1,
});
```


The following example shows a queue triggered [JavaScript function](functions-reference-node) that makes a copy of a blob. The function is triggered by a queue message that contains the name of the blob to copy. The new blob is named *{originalblobname}-Copy*.

```
const { app, input, output } = require('@azure/functions');
const blobInput = input.storageBlob({
path: 'samples-workitems/{queueTrigger}',
connection: 'MyStorageConnectionAppSetting',
});
const blobOutput = output.storageBlob({
path: 'samples-workitems/{queueTrigger}-Copy',
connection: 'MyStorageConnectionAppSetting',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [blobInput],
return: blobOutput,
handler: (queueItem, context) => {
return context.extraInputs.get(blobInput);
},
});
```


The following example shows a blob input binding, defined in the *function.json* file, which makes the incoming blob data available to the [PowerShell](functions-reference-powershell) function.

Here's the json configuration:

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "source/{name}",
"connection": "AzureWebJobsStorage"
}
]
}
```


Here's the function code:

```
# Input bindings are passed in via param block.
param([byte[]] $InputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger: Name: $($TriggerMetadata.Name) Size: $($InputBlob.Length) bytes"
```


This example uses SDK types to directly access the underlying `BlobClient`

object provided by the Blob storage input binding:

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="file")
@app.blob_input(
arg_name="client", path="PATH/TO/BLOB", connection="AzureWebJobsStorage"
)
def blob_input(req: func.HttpRequest, client: blob.BlobClient):
logging.info(
f"Python blob input function processed blob \n"
f"Properties: {client.get_blob_properties()}\n"
f"Blob content head: {client.download_blob().read(size=1)}"
)
return "ok"
```


For examples of using other SDK types, see the [ ContainerClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_storagestreamdownloader/function_app.py)

`StorageStreamDownloader`

[Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The code creates a copy of a blob.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobOutput1")
@app.route(route="file")
@app.blob_input(arg_name="inputblob",
path="PATH/TO/BLOB",
connection="CONNECTION_SETTING")
@app.blob_output(arg_name="outputblob",
path="PATH/TO/NEW/BLOB",
connection="CONNECTION_SETTING")
def main(req: func.HttpRequest, inputblob: str, outputblob: func.Out[str]):
logging.info(f'Python Queue trigger function processed {len(inputblob)} bytes')
outputblob.set(inputblob)
return "ok"
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-input).

Isolated worker process defines an input binding by using a `BlobInputAttribute`

attribute, which takes the following parameters:

| Parameter | Description |
|---|---|
BlobPath |
The path to the blob. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using decorators, the following properties on the `blob_input`

and `blob_output`

decorators define the Blob Storage triggers:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the blob in function code. |
`path` |
The path to the blob For the `blob_input` decorator, it's the blob read. For the `blob_output` decorator, it's the output or copy of the input blob. |
`connection` |
The storage account connection string. |
`data_type` |
For dynamically typed languages, specifies the underlying data type. Possible values are `string` , `binary` , or `stream` . For more detail, refer to the
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobInput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [input example](#example) for details.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `input.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `in` . Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. |
path |
The path to the blob. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

**dataType**`string`

, `binary`

, or `stream`

. For more detail, refer to the [triggers and bindings concepts](functions-triggers-bindings?tabs=python#trigger-and-binding-definitions).See the [Example section](#example) for complete examples.

## Usage

The binding types supported by Blob input depend on the extension package version and the C# modality used in your function app.

When you want the function to process a single blob, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)1When you want the function to process multiple blobs from a container, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` or `List<T>` where `T` is one of the single blob input binding types |
An array or list of multiple blobs. Each entry represents one blob from the container. You can also bind to any interfaces implemented by these types, such as `IEnumerable<T>` . |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/6.0.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small, since the entire blob contents are loaded into memory. For most blobs, use a `Stream`

or `BlobClient`

type. For more information, see [Concurrency and memory usage](functions-bindings-storage-blob-trigger#memory-usage-and-concurrency).

If you get an error message when trying to bind to one of the Storage SDK types, make sure that you have a reference to [the correct Storage SDK version](functions-bindings-storage-blob#tabpanel_2_functionsv1_in-process).

You can also use the [StorageAccountAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs/StorageAccountAttribute.cs) to specify the storage account to use. You can do this when you need to use a different storage account than other functions in the library. The constructor takes the name of an app setting that contains a storage connection string. The attribute can be applied at the parameter, method, or class level. The following example shows class level and method level:

```
[StorageAccount("ClassLevelStorageAppSetting")]
public static class AzureFunctions
{
[FunctionName("BlobTrigger")]
[StorageAccount("FunctionLevelStorageAppSetting")]
public static void Run( //...
{
....
}
```


The storage account to use is determined in the following order:

- The
`BlobTrigger`

attribute's`Connection`

property. - The
`StorageAccount`

attribute applied to the same parameter as the`BlobTrigger`

attribute. - The
`StorageAccount`

attribute applied to the function. - The
`StorageAccount`

attribute applied to the class. - The default storage account for the function app, which is defined in the
`AzureWebJobsStorage`

application setting.

The `@BlobInput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [input example](#example) for details.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

Access blob data via the parameter typed as [InputStream](/en-us/python/api/azure-functions/azure.functions.inputstream). Refer to the [input example](#example) for details.

Functions also supports Python SDK type bindings for Azure Blob storage, which lets you work with blob data using these underlying SDK types:

Note

Only synchronous SDK types are supported.

Important

SDK types support for Python is generally available and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to Azure Blobs. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). The connection string must be for a general-purpose storage account, not a [Blob storage account](../storage/common/storage-account-overview#types-of-storage-accounts).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [version 5.x or higher of the extension](functions-bindings-storage-blob#install-extension) ([bundle 3.x or higher](functions-bindings-storage-blob?tabs=extensionv3#install-bundle) for non-.NET language stacks), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob Service URI | `<CONNECTION_NAME_PREFIX>__serviceUri` 1 |
The data plane URI of the blob service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__blobServiceUri`

can be used as an alias. If the connection configuration will be used by a blob trigger, `blobServiceUri`

must also be accompanied by `queueServiceUri`

. See below.

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables. The URI can only designate the blob service. As an alternative, you can provide a URI specifically for each service, allowing a single connection to be used. If both versions are provided, the multi-service form is used. To configure the connection for multiple services, instead of `<CONNECTION_NAME_PREFIX>__serviceUri`

, set:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Blob Service URI | `<CONNECTION_NAME_PREFIX>__blobServiceUri` |
The data plane URI of the blob service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.blob.core.windows.net |
Queue Service URI (required for blob triggers2) |
`<CONNECTION_NAME_PREFIX>__queueServiceUri` |
The data plane URI of a queue service, using the HTTPS scheme. This value is only needed for blob triggers. | https://<storage_account_name>.queue.core.windows.net |

2 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue. In the `serviceUri`

form, the `AzureWebJobsStorage`

connection is used. However, when specifying `blobServiceUri`

, a queue service URI must also be provided with `queueServiceUri`

. It's recommended that you use the service from the same storage account as the blob service. You also need to make sure the trigger can read and write messages in the configured queue service by assigning a role like [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor).

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You need to create a role assignment that provides access to your blob container at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Blob Storage extension in normal operation. Your application may require further permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
and
1Extra permissions must also be granted to the AzureWebJobsStorage connection. 2 |

[Storage Blob Data Reader](../role-based-access-control/built-in-roles#storage-blob-data-reader)[Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner)1 The blob trigger handles failure across multiple retries by writing [poison blobs](functions-bindings-storage-blob-trigger#poison-blobs) to a queue on the storage account specified by the connection.

2 The AzureWebJobsStorage connection is used internally for blobs and queues that enable the trigger. If it's configured to use an identity-based connection, it needs extra permissions beyond the default requirement. The required permissions are covered by the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner), [Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor), and [Storage Account Contributor](../role-based-access-control/built-in-roles#storage-account-contributor) roles. To learn more, see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redislist -->

# RedisListTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Lists | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following sample polls the key `listTest`

.:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisListTrigger
{
public class SimpleListTrigger
{
private readonly ILogger<SimpleListTrigger> logger;
public SimpleListTrigger(ILogger<SimpleListTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleListTrigger))]
public void Run(
[RedisListTrigger(Common.connectionStringSetting, "listTest")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


The following sample polls the key `listTest`

at a localhost Redis instance at `redisLocalhost`

:

```
package com.function.RedisListTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleListTrigger {
@FunctionName("SimpleListTrigger")
public void run(
@RedisListTrigger(
name = "req",
connection = "redisConnectionString",
key = "listTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host $entry
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameter | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`INameResolver`

.`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`COUNT`

argument in [and](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`10`

`ListPopFromBeginning`

[, or to pop entries from the end using](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`true`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
"entry" | ||
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`listPopFromBeginning`

`true`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Property | Description | Optional | Default |
|---|---|---|---|
`type` |
Name of the trigger. | No | |
`listPopFromBeginning` |
Whether to delete the stream entries after the function has run. Set to `true` . |
Yes | `true` |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`INameResolver`

.`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

`in`

.See the Example section for complete examples.

## Usage

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function. The trigger polls Redis at a configurable fixed interval, and uses [ LPOP](https://redis.io/commands/lpop/) and

[to pop entries from the lists.](https://redis.io/commands/rpop/)

`RPOP`

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid -->

# Azure Event Grid bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This reference shows how to connect to Azure Event Grid using Azure Functions triggers and bindings.

Event Grid is an Azure service that sends HTTP requests to notify you about events that happen in publishers. A *publisher* is the service or resource that originates the event. For example, an Azure blob storage account is a publisher, and [a blob upload or deletion is an event](../storage/blobs/storage-blob-event-overview). Some [Azure services have built-in support for publishing events to Event Grid](../event-grid/concepts#event-sources).

Event *handlers* receive and process events. Azure Functions is one of several [Azure services that have built-in support for handling Event Grid events](../event-grid/overview#event-handlers). Functions provides an Event Grid trigger, which invokes a function when an event is received from Event Grid. A similar output binding can be used to send events from your function to an [Event Grid custom topic](../event-grid/post-to-custom-topic).

You can also use an HTTP trigger to handle Event Grid Events. To learn more, see [Receive events to an HTTP endpoint](../event-grid/receive-events). We recommend using the Event Grid trigger over HTTP trigger.

| Action | Type |
|---|---|
| Run a function when an Event Grid event is dispatched |
|

[Output binding](functions-bindings-event-grid-output)[HTTP endpoint](../event-grid/receive-events)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid), version 3.x.

## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

Considerations for the Event Grid extension:

- Event Grid extension versions earlier than 3.x don't support
[CloudEvents schema](../event-grid/cloudevents-schema#azure-functions). To consume this schema, instead use an HTTP trigger. - The Event Grid output binding is only available for Functions 2.x and higher.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to `Stream`

, and to types from [Azure.Messaging](/en-us/dotnet/api/azure.messaging) is in preview.

**Event Grid trigger**

When you want the function to process a single event, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the event into a plain-old CLR object (POCO) type. |
`string` |
The event as a string. |
1 |

[CloudEvent](/en-us/dotnet/api/azure.messaging.cloudevent)1[EventGridEvent](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridevent)1When you want the function to process a batch of events, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
`CloudEvent[]` 1,`EventGridEvent[]` 1,`string[]` ,`BinaryData[]` 1 |
An array of events from the batch. Each entry represents one event. |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventGrid 3.3.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid/3.3.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Grid output binding**

When you want the function to write a single event, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. |
`byte[]` |
The bytes of the event message. |
| JSON serializable types | An object representing a JSON event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventGridPublisherClient](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient) with other types from [Azure.Messaging.EventGrid](/en-us/dotnet/api/azure.messaging.eventgrid) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## host.json settings

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Event Grid trigger](functions-bindings-event-grid-trigger)[Event Grid output binding](functions-bindings-event-grid-output)[Run a function when an Event Grid event is dispatched](functions-bindings-event-grid-trigger)[Dispatch an Event Grid event](functions-bindings-event-grid-trigger)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-input -->

# Azure Web PubSub input bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Our extension provides two input binding targeting different needs.

-
To let a client connect to Azure Web PubSub Service, it must know the service endpoint URL and a valid access token. The

`WebPubSubConnection`

input binding produces required information, so client doesn't need to handle this token generation itself. The token is time-limited and can authenticate a specific user to a connection. Therefore, don't cache the token or share it between clients. An HTTP trigger working with this input binding can be used for clients to retrieve the connection information. -
When using Static Web Apps,

`HttpTrigger`

is the only supported trigger. In Web PubSub scenarios, the`WebPubSubContext`

input binding helps users deserialize upstream HTTP requests from the service under Web PubSub protocols. So customers can get similar results comparing to`WebPubSubTrigger`

to easily handle in functions. When used with`HttpTrigger`

, customer requires to configure the HttpTrigger exposed url in event handler accordingly.

`WebPubSubConnection`


### Example

The following example shows an HTTP trigger function that acquires Web PubSub connection information using the input binding and returns it over HTTP. In following example, the `UserId`

is passed in through client request query part like `?userid={User-A}`

.

```
[Function("WebPubSubConnectionInputBinding")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[WebPubSubConnectionInput(Hub = "<hub>", , UserId = "{query.userid}", Connection = "<web_pubsub_connection_name>")] WebPubSubConnection connectionInfo)
{
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteAsJsonAsync(connectionInfo);
return response;
}
```


```
const { app, input } = require('@azure/functions');
const connection = input.generic({
type: 'webPubSubConnection',
name: 'connection',
userId: '{query.userId}',
hub: '<hub>'
});
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [connection],
handler: async (request, context) => {
return { body: JSON.stringify(context.extraInputs.get('connection')) };
},
});
```


Create a folder *negotiate* and update *negotiate/function.json* and copy following JSON codes.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "webPubSubConnection",
"name": "connection",
"userId": "{query.userid}",
"hub": "<hub>",
"direction": "in"
}
]
}
```


Define function in *negotiate/ init.py*.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest, connection) -> func.HttpResponse:
return func.HttpResponse(connection)
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Get authenticated user ID

If the function is triggered by an authenticated client, you can add a user ID claim to the generated token. You can easily add authentication to a function app using App Service Authentication.

App Service Authentication sets HTTP headers named `x-ms-client-principal-id`

and `x-ms-client-principal-name`

that contain the authenticated user's client principal ID and name, respectively.

You can set the `UserId`

property of the binding to the value from either header using a binding expression: `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

```
[Function("WebPubSubConnectionInputBinding")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[WebPubSubConnectionInput(Hub = "<hub>", , UserId = "{headers.x-ms-client-principal-id}", Connection = "<web_pubsub_connection_name>")] WebPubSubConnection connectionInfo)
{
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteAsJsonAsync(connectionInfo);
return response;
}
```


```
const { app, input } = require('@azure/functions');
const connection = input.generic({
type: 'webPubSubConnection',
name: 'connection',
userId: '{headers.x-ms-client-principal-id}',
hub: '<hub>'
});
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [connection],
handler: async (request, context) => {
return { body: JSON.stringify(context.extraInputs.get('connection')) };
},
});
```


Create a folder *negotiate* and update *negotiate/function.json* and copy following JSON codes.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"type": "webPubSubConnection",
"name": "connection",
"userId": "{headers.x-ms-client-principal-id}",
"hub": "<hub>",
"direction": "in"
}
]
}
```


Define function in *negotiate/ init.py*.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest, connection) -> func.HttpResponse:
return func.HttpResponse(connection)
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Configuration

The following table explains the binding configuration properties that you set in the function.json file and the `WebPubSubConnection`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSubConnection` |
direction |
n/a | Must be set to `in` |
name |
n/a | Variable name used in function code for input connection binding object. |
hub |
Hub | Required - The value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
userId |
UserId | Optional - the value of the user identifier claim to be set in the access key token. |
clientProtocol |
ClientProtocol | Optional - The client protocol type. Valid values include `default` and `mqtt` . For MQTT clients, you must set it to `mqtt` . For other clients, you can omit the property or set it to `default` . |
connection |
Connection | Required - The name of the app setting that contains the Web PubSub Service connection string (defaults to "WebPubSubConnectionString"). |

### Usage

`WebPubSubConnection`

provides following properties.

| Binding Name | Binding Type | Description |
|---|---|---|
| BaseUri | Uri | Web PubSub client connection uri. |
| Uri | Uri | Absolute Uri of the Web PubSub connection, contains `AccessToken` generated base on the request. |
| AccessToken | string | Generated `AccessToken` based on request UserId and service information. |

`WebPubSubConnection`

provides following properties.

| Binding Name | Description |
|---|---|
| baseUrl | Web PubSub client connection uri. |
| url | Absolute Uri of the Web PubSub connection, contains `AccessToken` generated base on the request. |
| accessToken | Generated `AccessToken` based on request UserId and service information. |

Note

The Web PubSub extensions for Java isn't supported yet.

### More customization of generated token

Limited to the binding parameter types don't support a way to pass list nor array, the `WebPubSubConnection`

isn't fully supported with all the parameters server SDK has, especially `roles`

, and also includes `groups`

and `expiresAfter`

.

When customer needs to add roles or delay building the access token in the function, we suggest you to work with [server SDK for C#](/en-us/dotnet/api/overview/azure/messaging.webpubsub-readme).

```
[Function("WebPubSubConnectionCustomRoles")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req)
{
var serviceClient = new WebPubSubServiceClient(new Uri(endpoint), "<hub>", "<web-pubsub-connection-string>");
var userId = req.Query["userid"].FirstOrDefault();
// your method to get custom roles.
var roles = GetRoles(userId);
var url = await serviceClient.GetClientAccessUriAsync(TimeSpan.FromMinutes(5), userId, roles);
var response = req.CreateResponse(HttpStatusCode.OK);
response.WriteString(url.ToString());
return response;
}
```


When customer needs to add roles or delay building the access token in the function, we suggest you working with [server SDK for JavaScript](/en-us/javascript/api/overview/azure/web-pubsub).

```
const { app } = require('@azure/functions');
const { WebPubSubServiceClient } = require('@azure/web-pubsub');
app.http('negotiate', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
const serviceClient = new WebPubSubServiceClient(process.env.WebPubSubConnectionString, "<hub>");
let token = await serviceClient.getAuthenticationToken({ userId: req.query.userid, roles: ["webpubsub.joinLeaveGroup", "webpubsub.sendToGroup"] });
return { body: token.url };
},
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

`WebPubSubContext`


### Example

```
// validate method when upstream set as http://<func-host>/api/{event}
[Function("validate")]
public static HttpResponseData Validate(
[HttpTrigger(AuthorizationLevel.Anonymous, "options")] HttpRequestData req,
[WebPubSubContextInput] WebPubSubContext wpsReq)
{
return BuildHttpResponseData(req, wpsReq.Response);
}
// Respond AbuseProtection to put header correctly.
private static HttpResponseData BuildHttpResponseData(HttpRequestData request, SimpleResponse wpsResponse)
{
var response = request.CreateResponse();
response.StatusCode = (HttpStatusCode)wpsResponse.Status;
response.Body = response.Body;
foreach (var header in wpsResponse.Headers)
{
response.Headers.Add(header.Key, header.Value);
}
return response;
}
```


```
const { app, input } = require('@azure/functions');
const wpsContext = input.generic({
type: 'webPubSubContext',
name: 'wpsContext'
});
app.http('connect', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [wpsContext],
handler: async (request, context) => {
var wpsRequest = context.extraInputs.get('wpsContext');
return { "userId": wpsRequest.request.connectionContext.userId };
}
});
```


Note

Complete samples for this language are pending

Note

The Web PubSub extensions for Java isn't supported yet.

### Configuration

The following table explains the binding configuration properties that you set in the functions.json file and the `WebPubSubContext`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `webPubSubContext` . |
direction |
n/a | Must be set to `in` . |
name |
n/a | Variable name used in function code for input Web PubSub request. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for
`null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

### Usage

`WebPubSubContext`

provides following properties.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Request from client, see following table for details. | `WebPubSubConnectionContext` from request header and other properties deserialized from request body describe the request, for example, `Reason` for `DisconnectedEventRequest` . |
| response | `HttpResponseMessage` |
Extension builds response mainly for `AbuseProtection` and errors cases. |
- |
| errorMessage | string | Describe the error details when processing the upstream request. | - |
| hasError | bool | Flag to indicate whether it's a valid Web PubSub upstream request. | - |
| isPreflight | bool | Flag to indicate whether it's a preflight request of `AbuseProtection` . |
- |

For `WebPubSubEventRequest`

, it's deserialized to different classes that provide different information about the request scenario. For `PreflightRequest`

or not valid cases, user can check the flags `IsPreflight`

and `HasError`

to know. We suggest you to return system build response `WebPubSubContext.Response`

directly, or customer can log errors on demand. In different scenarios, customer can read the request properties as following.

| Derived Class | Description | Properties |
|---|---|---|
`PreflightRequest` |
Used in `AbuseProtection` when `IsPreflight` is true |
- |
`ConnectEventRequest` |
Used in system `Connect` event type |
Claims, Query, Subprotocols, ClientCertificates |
`ConnectedEventRequest` |
Used in system `Connected` event type |
- |
`UserEventRequest` |
Used in user event type | Data, DataType |
`DisconnectedEventRequest` |
Used in system `Disconnected` event type |
Reason |

Note

Though the

`WebPubSubContext`

is an input binding provides similar request deserialize way under`HttpTrigger`

comparing to`WebPubSubTrigger`

, there's limitations, i.e. connection state post merge isn't supported. The return response is still respected by the service side, but users require to build the response themselves. If users have needs to set the event response, you should return a`HttpResponseMessage`

contains`ConnectEventResponse`

or messages for user event asresponse bodyand put connection state with key`ce-connectionstate`

inresponse header.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json -->

# host.json reference for Azure Functions 2.x and later

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The host.json metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available starting with version 2.x of the Azure Functions runtime.

Note

This article is for Azure Functions 2.x and later versions. For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

Other function app configuration options are managed depending on where the function app runs:

**Deployed to Azure**: in your[application settings](functions-app-settings)**On your local computer**: in the[local.settings.json](functions-develop-local#local-settings-file)file.

Configurations in host.json related to bindings are applied equally to each function in the function app.

You can also [override or apply settings per environment](#override-hostjson-values) using application settings.

## Sample host.json file

The following sample *host.json* file for version 2.x+ has all possible options specified (excluding any that are for internal use only).

```
{
"version": "2.0",
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"blobs": {},
"cosmosDb": {},
"durableTask": {},
"eventHubs": {},
"http": {},
"queues": {},
"sendGrid": {},
"serviceBus": {}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"evaluationInterval": "01:00:00",
"initialSamplingPercentage": 100.0,
"samplingPercentageIncreaseTimeout" : "00:00:01",
"samplingPercentageDecreaseTimeout" : "00:00:01",
"minSamplingPercentage": 0.1,
"maxSamplingPercentage": 100.0,
"movingAverageRatio": 1.0,
"excludedTypes" : "Dependency;Event",
"includedTypes" : "PageView;Trace"
},
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
},
"enableLiveMetrics": true,
"enableDependencyTracking": true,
"enablePerformanceCountersCollection": true,
"httpAutoCollectionOptions": {
"enableHttpTriggerExtendedInfoCollection": true,
"enableW3CDistributedTracing": true,
"enableResponseHeaderInjection": true
},
"snapshotConfiguration": {
"agentEndpoint": null,
"captureSnapshotMemoryWeight": 0.5,
"failedRequestLimit": 3,
"handleUntrackedExceptions": true,
"isEnabled": true,
"isEnabledInDeveloperMode": false,
"isEnabledWhenProfiling": true,
"isExceptionSnappointsEnabled": false,
"isLowPrioritySnapshotUploader": true,
"maximumCollectionPlanSize": 50,
"maximumSnapshotsRequired": 3,
"problemCounterResetInterval": "24:00:00",
"provideAnonymousTelemetry": true,
"reconnectInterval": "00:15:00",
"shadowCopyFolder": null,
"shareUploaderProcess": true,
"snapshotInLowPriorityThread": true,
"snapshotsPerDayLimit": 30,
"snapshotsPerTenMinutesLimit": 1,
"tempFolder": null,
"thresholdForSnapshotting": 1,
"uploaderProxy": null
}
}
},
"managedDependency": {
"enabled": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"telemetryMode": "OpenTelemetry",
"watchDirectories": [ "Shared", "Test" ],
"watchFiles": [ "myFile.txt" ]
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

This setting is a child of [logging](#logging).

Controls options for Application Insights, including [sampling options](configure-monitoring#configure-sampling).

For the complete JSON structure, see the earlier [example host.json file](#sample-hostjson-file).

Note

Log sampling may cause some executions to not show up in the Application Insights monitor blade. To avoid log sampling, add `excludedTypes: "Request"`

to the `samplingSettings`

value.

| Property | Default | Description |
|---|---|---|
| samplingSettings | n/a | See
|

[applicationInsights.dependencyTrackingOptions](#applicationinsightsdependencytrackingoptions).[applicationInsights.samplingSettings.excludedTypes](#applicationinsightssamplingsettings), For more information, see see[Select and filter your metrics](/en-us/azure/azure-monitor/app/live-stream#select-and-filter-your-metrics).[applicationInsights.httpAutoCollectionOptions](#applicationinsightshttpautocollectionoptions).[applicationInsights.snapshotConfiguration](#applicationinsightssnapshotconfiguration).### applicationInsights.samplingSettings

For more information about these settings, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 20 | The target number of telemetry items logged per second on each server host. If your app runs on many hosts, reduce this value to remain within your overall target rate of traffic. |
| evaluationInterval | 01:00:00 | The interval at which the current rate of telemetry is reevaluated. Evaluation is performed as a moving average. You might want to shorten this interval if your telemetry is liable to sudden bursts. |
| initialSamplingPercentage | 100.0 | The initial sampling percentage applied at the start of the sampling process to dynamically vary the percentage. Don't reduce value while you're debugging. |
| samplingPercentageIncreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to raise sampling percentage again to capture more data. |
| samplingPercentageDecreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to lower sampling percentage again to capture less data. |
| minSamplingPercentage | 0.1 | As sampling percentage varies, this property determines the minimum allowed sampling percentage. |
| maxSamplingPercentage | 100.0 | As sampling percentage varies, this property determines the maximum allowed sampling percentage. |
| movingAverageRatio | 1.0 | In the calculation of the moving average, the weight assigned to the most recent value. Use a value equal to or less than 1. Smaller values make the algorithm less reactive to sudden changes. |
| excludedTypes | null | A semi-colon delimited list of types that you don't want to be sampled. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . All instances of the specified types are transmitted; the types that aren't specified are sampled. |
| includedTypes | null | A semi-colon delimited list of types that you want to be sampled; an empty list implies all types. Type listed in `excludedTypes` override types listed here. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . Instances of the specified types are sampled; the types that aren't specified or implied are transmitted without sampling. |

### applicationInsights.httpAutoCollectionOptions

| Property | Default | Description |
|---|---|---|
| enableHttpTriggerExtendedInfoCollection | true | Enables or disables extended HTTP request information for HTTP triggers: incoming request correlation headers, multi-instrumentation keys support, HTTP method, path, and response. |
| enableW3CDistributedTracing | true | Enables or disables support of W3C distributed tracing protocol (and turns on legacy correlation schema). Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. If `enableHttpTriggerExtendedInfoCollection` is false, this flag applies to outgoing requests only, not incoming requests. |
| enableResponseHeaderInjection | true | Enables or disables injection of multi-component correlation headers into responses. Enabling injection allows Application Insights to construct an Application Map to when several instrumentation keys are used. Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. This setting doesn't apply if `enableHttpTriggerExtendedInfoCollection` is false. |

### applicationInsights.dependencyTrackingOptions

| Property | Default | Description |
|---|---|---|
| enableSqlCommandTextInstrumentation | false | Enables collection of the full text of SQL queries, which is disabled by default. For more information on collecting SQL query text, see
|

### applicationInsights.snapshotConfiguration

For more information on snapshots, see [Debug snapshots on exceptions in .NET apps](/en-us/azure/azure-monitor/app/snapshot-debugger) and [Troubleshoot problems enabling Application Insights Snapshot Debugger or viewing snapshots](/en-us/troubleshoot/azure/azure-monitor/app-insights/snapshot-debugger-troubleshoot).

| Property | Default | Description |
|---|---|---|
| agentEndpoint | null | The endpoint used to connect to the Application Insights Snapshot Debugger service. If null, a default endpoint is used. |
| captureSnapshotMemoryWeight | 0.5 | The weight given to the current process memory size when checking if there's enough memory to take a snapshot. The expected value is a greater than 0 proper fraction (0 < CaptureSnapshotMemoryWeight < 1). |
| failedRequestLimit | 3 | The limit on the number of failed requests to request snapshots before the telemetry processor is disabled. |
| handleUntrackedExceptions | true | Enables or disables tracking of exceptions that aren't tracked by Application Insights telemetry. |
| isEnabled | true | Enables or disables snapshot collection |
| isEnabledInDeveloperMode | false | Enables or disables snapshot collection is enabled in developer mode. |
| isEnabledWhenProfiling | true | Enables or disables snapshot creation even if the Application Insights Profiler is collecting a detailed profiling session. |
| isExceptionSnappointsEnabled | false | Enables or disables filtering of exceptions. |
| isLowPrioritySnapshotUploader | true | Determines whether to run the SnapshotUploader process at below normal priority. |
| maximumCollectionPlanSize | 50 | The maximum number of problems that we can track at any time in a range from one to 9999. |
| maximumSnapshotsRequired | 3 | The maximum number of snapshots collected for a single problem, in a range from one to 999. A problem may be thought of as an individual throw statement in your application. Once the number of snapshots collected for a problem reaches this value, no more snapshots will be collected for that problem until problem counters are reset (see `problemCounterResetInterval` ) and the `thresholdForSnapshotting` limit is reached again. |
| problemCounterResetInterval | 24:00:00 | How often to reset the problem counters in a range from one minute to seven days. When this interval is reached, all problem counts are reset to zero. Existing problems that have already reached the threshold for doing snapshots, but haven't yet generated the number of snapshots in `maximumSnapshotsRequired` , remain active. |
| provideAnonymousTelemetry | true | Determines whether to send anonymous usage and error telemetry to Microsoft. This telemetry may be used if you contact Microsoft to help troubleshoot problems with the Snapshot Debugger. It's also used to monitor usage patterns. |
| reconnectInterval | 00:15:00 | How often we reconnect to the Snapshot Debugger endpoint. Allowable range is one minute to one day. |
| shadowCopyFolder | null | Specifies the folder to use for shadow copying binaries. If not set, the folders specified by the following environment variables are tried in order: Fabric_Folder_App_Temp, LOCALAPPDATA, APPDATA, TEMP. |
| shareUploaderProcess | true | If true, only one instance of SnapshotUploader will collect and upload snapshots for multiple apps that share the InstrumentationKey. If set to false, the SnapshotUploader will be unique for each (ProcessName, InstrumentationKey) tuple. |
| snapshotInLowPriorityThread | true | Determines whether or not to process snapshots in a low IO priority thread. Creating a snapshot is a fast operation but, in order to upload a snapshot to the Snapshot Debugger service, it must first be written to disk as a minidump. That happens in the SnapshotUploader process. Setting this value to true uses low-priority IO to write the minidump, which won't compete with your application for resources. Setting this value to false speeds up minidump creation at the expense of slowing down your application. |
| snapshotsPerDayLimit | 30 | The maximum number of snapshots allowed in one day (24 hours). This limit is also enforced on the Application Insights service side. Uploads are rate limited to 50 per day per application (that is, per instrumentation key). This value helps prevent creating additional snapshots that will eventually be rejected during upload. A value of zero removes the limit entirely, which isn't recommended. |
| snapshotsPerTenMinutesLimit | 1 | The maximum number of snapshots allowed in 10 minutes. Although there's no upper bound on this value, exercise caution increasing it on production workloads because it could impact the performance of your application. Creating a snapshot is fast, but creating a minidump of the snapshot and uploading it to the Snapshot Debugger service is a much slower operation that will compete with your application for resources (both CPU and I/O). |
| tempFolder | null | Specifies the folder to write minidumps and uploader log files. If not set, then %TEMP%\Dumps is used. |
| thresholdForSnapshotting | 1 | How many times Application Insights needs to see an exception before it asks for snapshots. |
| uploaderProxy | null | Overrides the proxy server used in the Snapshot Uploader process. You may need to use this setting if your application connects to the internet via a proxy server. The Snapshot Collector runs within your application's process and will use the same proxy settings. However, the Snapshot Uploader runs as a separate process and you may need to configure the proxy server manually. If this value is null, then Snapshot Collector will attempt to autodetect the proxy's address by examining `System.Net.WebRequest.DefaultWebProxy` and passing on the value to the Snapshot Uploader. If this value isn't null, then autodetection isn't used and the proxy server specified here will be used in the Snapshot Uploader. |

## blobs

Configuration settings can be found in [Storage blob triggers and bindings](functions-bindings-storage-blob#hostjson-settings).

## console

This setting is a child of [logging](#logging). It controls the console logging when not in debugging mode.

```
{
"logging": {
...
"console": {
"isEnabled": false,
"DisableColors": true
},
...
}
}
```


| Property | Default | Description |
|---|---|---|
| DisableColors | false | Suppresses log formatting in the container logs on Linux. Set to true if you're seeing unwanted ANSI control characters in the container logs when running on Linux. |
| isEnabled | false | Enables or disables console logging. |

## Azure Cosmos DB

Configuration settings can be found in [Azure Cosmos DB triggers and bindings](functions-bindings-cosmosdb-v2#hostjson-settings).

## customHandler

Configuration settings for a custom handler. For more information, see [Azure Functions custom handlers](functions-custom-handlers#configuration).

```
"customHandler": {
"description": {
"defaultExecutablePath": "server",
"workingDirectory": "handler",
"arguments": [ "--port", "%FUNCTIONS_CUSTOMHANDLER_PORT%" ]
},
"enableForwardingHttpRequest": false
}
```


| Property | Default | Description |
|---|---|---|
| defaultExecutablePath | n/a | The executable to start as the custom handler process. It's a required setting when using custom handlers and its value is relative to the function app root. |
| workingDirectory | function app root |
The working directory in which to start the custom handler process. It's an optional setting and its value is relative to the function app root. |
| arguments | n/a | An array of command line arguments to pass to the custom handler process. |
| enableForwardingHttpRequest | false | If set, all functions that consist of only an HTTP trigger and HTTP output is forwarded the original HTTP request instead of the custom handler
|

## durableTask

Configuration setting can be found in [bindings for Durable Functions](durable/durable-functions-bindings#host-json).

## concurrency

Enables dynamic concurrency for specific bindings in your function app. For more information, see [Dynamic concurrency](functions-concurrency#dynamic-concurrency).

```
{
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicConcurrencyEnabled | false | Enables dynamic concurrency behaviors for all triggers supported by this feature, which is off by default. |
| snapshotPersistenceEnabled | true | Learned concurrency values are periodically persisted to storage so new instances start from those values instead of starting from 1 and having to redo the learning. |

## eventHub

Configuration settings can be found in [Event Hub triggers and bindings](functions-bindings-event-hubs#host-json).

## extensions

Property that returns an object that contains all of the binding-specific settings, such as [http](#http) and [eventHub](#eventhub).

## extensionBundle

Extension bundles let you add a compatible set of Functions binding extensions to your function app. To learn more, see [Extension bundles for local development](extension-bundles).

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

The following properties are available in `extensionBundle`

:

| Property | Description |
|---|---|
`id` |
The namespace for Azure Functions extension bundles. |
`version` |
The version range of the bundle to install. The Azure Functions runtime always chooses the maximum permissible version that the version range or interval defines. For example, a `version` value range of `[4.0.0, 5.0.0)` allows all bundle versions from 4.0.0 up to (but not including) 5.0.0. For more information, see the
|

Tip

You might also see the version range defined in your *host.json* as `[4.*, 5.0.0)`

, which is interpreted the same as `[4.0.0, 5.0.0)`

.

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all function executions. It follows the [timespan string format](/en-us/dotnet/fundamentals/runtime-libraries/system-timespan-parse). A value of `-1`

indicates unbounded execution, but keeping a fixed upper bound is recommended.

```
{
"functionTimeout": "00:05:00"
}
```


The format of the timespan string needs to follow the syntax `[d.]hh:mm:ss`

and the valid values are:

- d = days (optional)
- hh = hours (0–23)
- mm = minutes (0–59)
- ss = seconds (0–59)

Tip

When you need to set a 24-hour timeout, you must define it as one day (`"1.00:00:00"`

) instead of 24 hours (`"24:00:00"`

). You might also use `"23:59:59"`

.

For more information on the default and maximum values for specific plans, see [Function app timeout duration](functions-scale#timeout).

## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used in conjunction with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings can be found in [http triggers and bindings](functions-bindings-http-webhook#hostjson-settings).

## logging

Controls the logging behaviors of the function app, including Application Insights.

```
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"console": {
...
},
"applicationInsights": {
...
}
}
```


| Property | Default | Description |
|---|---|---|
| fileLoggingMode | debugOnly | Determines the file logging behavior when running in Azure. Options are `never` , `always` , and `debugOnly` . This setting isn't used when running locally. When possible, you should use Application Insights when debugging your functions in Azure. Using `always` negatively impacts your app's cold start behavior and data throughput. The default `debugOnly` setting generates log files when you're debugging using the Azure portal. |
| logLevel | n/a | Object that defines the log category filtering for functions in the app. This setting lets you filter logging for specific functions. For more information, see
|

[console](#console)logging setting.[applicationInsights](#applicationinsights)setting.## managedDependency

Managed dependency is a feature that is currently only supported with PowerShell based functions. It enables dependencies to be automatically managed by the service. When the `enabled`

property is set to `true`

, the `requirements.psd1`

file is processed. Dependencies are updated when any minor versions are released. For more information, see [Managed dependency](functions-reference-powershell#dependency-management) in the PowerShell article.

```
{
"managedDependency": {
"enabled": true
}
}
```


## queues

Configuration settings can be found in [Storage queue triggers and bindings](functions-bindings-storage-queue#host-json).

## sendGrid

Configuration setting can be found in [SendGrid triggers and bindings](functions-bindings-sendgrid#host-json).

## serviceBus

Configuration setting can be found in [Service Bus triggers and bindings](functions-bindings-service-bus).

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime will try to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## telemetryMode

*This feature is currently in preview.*

Used to enable output of logs and traces in an OpenTelemetry output format to one or more endpoints that support OpenTelemetry. When this setting is set to `OpenTelemetry`

, OpenTelemetry output is used. By default without this setting, all logs, traces, and events are sent to Application Insights using the standard outputs. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## version

This value indicates the schema version of host.json. The version string `"version": "2.0"`

is required for a function app that targets the v2 runtime, or a later version. There are no host.json schema changes between v2 and v3.

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```


## watchFiles

An array of one or more names of files that are monitored for changes that require your app to restart. This guarantees that when code in these files is changed, the updates are picked up by your functions.

```
{
"watchFiles": [ "myFile.txt" ]
}
```


## Override host.json values

There may be instances where you wish to configure or modify specific settings in a host.json file for a specific environment, without changing the host.json file itself. You can override specific host.json values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent host.json setting located at `path.to.setting`

in the JSON. When expressed as an application setting, the dot (`.`

) used to indicate JSON hierarchy is replaced by a double underscore (`__`

).

For example, say that you wanted to disable Application Insight sampling when running locally. If you changed the local host.json file to disable Application Insights, this change might get pushed to your production app during deployment. The safer way to do this is to instead create an application setting as `"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"`

in the `local.settings.json`

file. You can see this in the following `local.settings.json`

file, which doesn't get published:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "{storage-account-connection-string}",
"FUNCTIONS_WORKER_RUNTIME": "{language-runtime}",
"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"
}
}
```


Overriding host.json settings using environment variables follows the ASP.NET Core naming conventions. When the element structure includes an array, the numeric array index should be treated as an additional element name in this path. For more information, see [Naming of environment variables](/en-us/aspnet/core/fundamentals/configuration/#naming-of-environment-variables).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-database-changes-azure-sqldb -->

# Quickstart: Respond to Azure SQL Database changes using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Quickstart, you use Visual Studio Code to build an app that responds to changes in an Azure SQL Database table. After testing the code locally, you deploy it to a new serverless function app running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) extension with Visual Studio Code to simplify initializing and verifying your project code locally, and deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

Important

While responding to [changes in an Azure SQL database](functions-bindings-azure-mysql-trigger) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

- The
[SQL Server (mssql) extension](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)for Visual Studio Code.

## Initialize the project

You can use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace in which you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, and then choose**Select a template**.When prompted, search for and select

`Azure Functions with SQL Triggers and Bindings`

.When prompted, enter a unique environment name, such as

`sqldbchanges`

.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

Before you can run your app locally, you must create the resources in Azure.

## Create Azure resources

This project is configured to use the `azd provision`

command to create a function app in a Flex Consumption plan, along with other required Azure resources that follow current best practices.

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, and then sign in using your Azure account.Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Provision Azure resources (provision)`

to create the required Azure resources.When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Select the subscription in which you want your resources to be created. *location*deployment parameterAzure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*deployment parameterWhile the template supports creating resources inside a virtual network, to simplify deployment and testing, choose `False`

.

The `azd provision`

command uses your response to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:

- Flex Consumption plan and function app
- Azure SQL Database (default name: ToDo)
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Post-provision hooks also generate the *local.settings.json* file, which is required to run locally. This file contains the settings required to connect to your database in Azure.

## Review the code (optional)

The sample defines two functions:

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httptrigger-sql-output` |
|

`ToDo`

table.`ToDoTrigger`

[sql_trigger.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/sql_trigger.cs)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/ToDoItem.cs).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`http_trigger_sql_output` |
|

`ToDo`

table.`httptrigger-sql-output`

[sql_trigger_todo](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/function_app.py#L15C5-L15C21)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [todo_item.py](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/todo_item.py).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httpTriggerSqlOutput` |
|

`ToDo`

table.`sqlTriggerToDo`

[sql_trigger.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/functions/sql_trigger.ts)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/models/ToDoItem.ts).

Both functions use the app-level `AZURE_SQL_CONNECTION_STRING_KEY_*`

environment variables that define an identity-based connection to the Azure SQL Database instance using Microsoft Entra ID authentication. These environment variables are created for you both in Azure (function app settings) and locally (local.settings.json) during the `azd provision`

operation.

## Connect to the SQL database

You can use the SQL Server (mssql) extension for Visual Studio Code to connect to the new database. This extension helps you make updates in the `ToDo`

table to run the SQL trigger function.

Press

`F1`and in the command palette search for and run the command`MS SQL: Add Connection`

.In the

**Connection dialog**, change**Input type**to**Browse Azure**and then set these remaining options:Option Choose Description **Server**Your SQL Server instance By default, all servers accessible to your Azure account are displayed. Use **Subscription**,**Resource group**, and**Location**to help filter the servers list.**Database**`ToDo`

The database created during the provisioning process. **Authentication type****Microsoft Entra ID**If you aren't already signed-in, select **Sign in**and sign in to your Azure account.**Tenant ID**The specific account tenant. If your account has more than one tenant, choose the correct tenant for your subscription. Select

**Connect**to connect to your database. The connection uses your local user account, which is granted admin permissions in the hosting server and mapped to`dbo`

in the database.In the

**SQL Server**view, locate and expand**Connections**and then your new server in SQL Server explorer. Expand**Tables**and verify that the`ToDo`

table exists. If it doesn't exist, you might need run`azd provision`

again and check for errors.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to your new function app in Azure.

Press

`F1`and in the command palette search for and run the command`Azurite: Start`

.To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar.The

**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the function that's running locally.

With the app running, you can verify and debug both function triggers.

To verify the HTTP trigger function that writes to a SQL output binding:

Copy this JSON object, which you can also find in the

`test.http`

project file:`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

This data represents a row that you insert in your SQL database when you call the HTTP endpoint. The output binding translates the data object into an

`INSERT`

operation in the database.With the app running, in the

**Azure**view under**Workspace**expand**Local project**>**Functions**.Right-select your HTTP function (or

`Ctrl`+click on macOS), select**Execute function now**, paste the copied JSON data, and press`Enter`.The function handles the HTTP request and writes the item to the connected SQL database and returns the created object.

Back in the SQL Server explorer, right-select the

`ToDo`

table (or`Ctrl`+click on macOS), and choose**Select Top 1000**. When the query executes, it returns the inserted or updated row.Repeat Step 3 and resend the same data object with the same ID. This time, the output binding performs an

`UPDATE`

operation instead of an`INSERT`

and modifies the existing row in the database.

When you're done, type `Ctrl`+`C` in the terminal to stop the Core Tools process.

## Deploy to Azure

You can run the `azd deploy`

command from Visual Studio Code to deploy the project code to your already provisioned resources in Azure.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Deploy to Azure (deploy)`

.The

`azd deploy`

command packages and deploys your code to the deployment container. The app is then started and runs in the deployed package.After the command completes successfully, your app is running in Azure. Make a note of the

`Endpoint`

value, which is the URL of your function app running in Azure.

## Invoke the function on Azure

In Visual Studio Code, press

`F1`and in the command palette search for and run the command`Azure: Open in portal`

, select`Function app`

, and choose your new app. Sign in with your Azure account, if necessary.Select

**Log stream**in the left pane, which connects to the Application Insights logs for your app.Return to Visual Studio Code to run both the functions in Azure.


Press

`F1`to open the command palette, search for and run the command`Azure Functions: Execute Function Now...`

.Search for and select your remote function app from the list, then select the HTTP trigger function.

As before, paste your JSON object data in

**Enter payload body**and press`Enter`.`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

To perform an

`INSERT`

instead of an`UPDATE`

, replace the`id`

with a new GUID value.Return to the portal and view the execution output in the log window.


## Clean up resources

When you're done working with your function app and related resources, you can use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-diagnostics -->

# Azure Functions diagnostics overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you’re running a function app, you want to be prepared for any issues that may arise, from 4xx errors to trigger failures. Azure Functions diagnostics is an intelligent and interactive experience to help you troubleshoot your function app with no configuration or extra cost. When you do run into issues with your function app, Azure Functions diagnostics points out what’s wrong. It guides you to the right information to more easily and quickly troubleshoot and resolve the issue. This article shows you the basics of how to use Azure Functions diagnostics to more quickly diagnose and solve common function app issues.

## Start Azure Functions diagnostics

To start Azure Functions diagnostics:

Navigate to your function app in the

[Azure portal](https://portal.azure.com).Select

**Diagnose and solve problems**to open Azure Functions diagnostics.Choose a category that best describes the issue of your function app by using the keywords in the homepage tile. You can also type a keyword that best describes your issue in the search bar. For example, you could type

`execution`

to see a list of diagnostic reports related to your function app execution and open them directly from the homepage.

## Use the Interactive interface

Once you select a homepage category that best aligns with your function app's problem, Azure Functions diagnostics' interactive interface, named Genie, can guide you through diagnosing and solving problem of your app. You can use the tile shortcuts provided by Genie to view the full diagnostic report of the problem category that you're interested in. The tile shortcuts provide you a direct way of accessing your diagnostic metrics.


After selecting a tile, you can see a list of topics related to the issue described in the tile. These topics provide snippets of notable information from the full report. Select any of these topics to investigate the issues further. Also, you can select **View Full Report** to explore all the topics on a single page.


## View a diagnostic report

After you choose a topic, you can view a diagnostic report specific to your function app. Diagnostic reports use status icons to indicate if there are any specific issues with your app. You see detailed description of the issue, recommended actions, related-metrics, and helpful docs. Customized diagnostic reports are generated from a series of checks run on your function app. Diagnostic reports can be a useful tool for pinpointing problems in your function app and guiding you towards resolving the issue.

## Find the problem code

For script-based functions, you can use **Function Execution and Errors** under **Function App Down or Reporting Errors** to narrow down on the line of code causing exceptions or errors. You can use this tool for getting to the root cause and fixing issues from a specific line of code. This option isn't available for precompiled C# and Java functions.


## Next steps

You can ask questions or provide feedback on Azure Functions diagnostics at [UserVoice](https://feedback.azure.com/d365community/forum/9df02822-f224-ec11-b6e6-000d3a4f0da0). Include `[Diag]`

in the title of your feedback.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-openapi-definition -->

# Expose serverless APIs from HTTP endpoints using Azure API Management

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Azure API Management in the portal to let you expose your HTTP trigger function endpoints as REST APIs. These APIs are described using an OpenAPI definition. This JSON (or YAML) file contains information about what operations are available in an API. It includes details about how the request and response data for the API should be structured. By integrating your function app, you can have API Management generate these OpenAPI definitions.

This article shows you how to integrate your function app with API Management. This integration works for function apps developed in any [supported language](supported-languages). You can also [import your function app from Azure API Management](../api-management/import-function-app-as-api).

For C# class library functions, you can also [use Visual Studio](openapi-apim-integrate-visual-studio) to create and publish serverless API that integrate with API Management.

## Create the API Management instance

To create an API Management instance linked to your function app:

Select the function app, choose

**API Management**from the left menu, and then select**Create new**under**API Management**.Use the API Management settings as specified in the following table:

Setting Suggested value Description **Subscription**Your subscription The subscription under which this new resource is created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The same resource as your function app, which should get set for you. **Region**Location of the service Consider choosing the same location as your function app. **Resource name**Globally unique name A name is generated based on the name of your function app. **Organization name**Contoso The name of the organization used in the developer portal and for email notifications. **Administrator email**your email Email that received system notifications from API Management. **Pricing tier**Consumption Consumption tier isn't available in all regions. For complete pricing details, see the [API Management pricing page](https://azure.microsoft.com/pricing/details/api-management/)Choose

**Review + create**and then**Create**to create the API Management instance, which may take several minutes.

## Import functions

After the API Management instance is created, you can import your HTTP triggered function endpoints. This example imports an endpoint named TurbineRepair.

In the API Management page, select

**Link API**.The

**Import Azure Functions**opens with the**TurbineRepair**function highlighted. Choose**Select**to continue.In the

**Create from Function App**page, accept the defaults, and then select**Create**. Azure creates the API for the function.

## Download the OpenAPI definition

After your functions have been imported, you can download the OpenAPI definition from the API Management instance.

Select

**Download OpenAPI definition**at the top of the page.Save the downloaded JSON file, and then open it. Review the definition.


## Next steps

You can now refine the definition in API Management in the portal. You can also [learn more about API Management](../api-management/api-management-key-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-maven-intellij -->

# Create your first Java function in Azure using IntelliJ

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Java and IntelliJ to create an Azure function.

Specifically, this article shows you:

- How to create an HTTP-triggered Java function in an IntelliJ IDEA project.
- Steps for testing and debugging the project in the integrated development environment (IDE) on your own computer.
- Instructions for deploying the function project to Azure Functions.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An
[Azure supported Java Development Kit (JDK)](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21. (Java 21 is currently supported on Linux only) - An
[IntelliJ IDEA](https://www.jetbrains.com/idea/download/)Ultimate Edition or Community Edition installed [Maven 3.5.0+](https://maven.apache.org/download.cgi)- Latest
[Function Core Tools](https://github.com/Azure/azure-functions-core-tools)

## Install plugin and sign in

To install the Azure Toolkit for IntelliJ and then sign in, follow these steps:

In IntelliJ IDEA's

**Settings/Preferences**dialog (Ctrl+Alt+S), select**Plugins**. Then, find the**Azure Toolkit for IntelliJ**in the**Marketplace**and select**Install**. After it's installed, select**Restart**to activate the plugin.To sign in to your Azure account, open the

**Azure Explorer**sidebar, and then select the**Azure Sign In**icon in the bar on top (or from the IDEA menu, select**Tools > Azure > Azure Sign in**).In the

**Azure Sign In**window, select**OAuth 2.0**, and then select**Sign in**. For other sign-in options, see[Sign-in instructions for the Azure Toolkit for IntelliJ](/en-us/azure/developer/java/toolkit-for-intellij/sign-in-instructions).In the browser, sign in with your account and then go back to IntelliJ. In the

**Select Subscriptions**dialog box, select the subscriptions that you want to use, then select**Select**.

## Create your local project

To use Azure Toolkit for IntelliJ to create a local Azure Functions project, follow these steps:

Open IntelliJ IDEA's

**Welcome**dialog, select**New Project**to open a new project wizard, then select**Azure Functions**.Select

**Http Trigger**, then select**Next**and follow the wizard to go through all the configurations in the following pages. Confirm your project location, then select**Finish**. IntelliJ IDEA then opens your new project.

## Run the project locally

To run the project locally, follow these steps:

Important

You must have the JAVA_HOME environment variable set correctly to the JDK directory that is used during code compiling using Maven. Make sure that the version of the JDK is at least as high as the `Java.version`

setting.

Navigate to

*src/main/java/org/example/functions/HttpTriggerJava.java*to see the code generated. Beside line 17, you should see a green**Run**button. Select it and then select**Run 'Functions-azur...'**. You should see your function app running locally with a few logs.You can try the function by accessing the displayed endpoint from browser, such as

`http://localhost:7071/api/HttpTriggerJava?name=Azure`

.The log is also displayed in your IDEA. Stop the function app by selecting

**Stop**.

## Debug the project locally

To debug the project locally, follow these steps:

Select the

**Debug**button in the toolbar. If you don't see the toolbar, enable it by choosing**View**>**Appearance**>**Toolbar**.Select line 20 of the file

*src/main/java/org/example/functions/HttpTriggerJava.java*to add a breakpoint. Access the endpoint`http://localhost:7071/api/HttpTriggerJava?name=Azure`

again and you should find that the breakpoint is hit. You can then try more debug features like**Step**,**Watch**, and**Evaluation**. Stop the debug session by selecting**Stop**.

## Create the function app in Azure

Use the following steps create a function app and related resources in your Azure subscription:

In Azure Explorer in your IDEA, right-click

**Function App**and then select**Create**.Select

**More Settings**and provide the following information at the prompts:Prompt Selection **Subscription**Choose the subscription to use. **Resource Group**Choose the resource group for your function app. **Name**Specify the name for a new function app. Here you can accept the default value. **Platform**Select **Windows-Java 17**or another platform as appropriate.**Region**For better performance, choose a [region](https://azure.microsoft.com/regions/)near you.**Hosting Options**Choose the hosting options for your function app. **Plan**Choose the App Service plan pricing tier you want to use, or select **+**to create a new App Service plan.Important

To create your app in the Flex Consumption plan, select

**Flex Consumption**. The[Flex Consumption plan](flex-consumption-plan)is currently in preview.Select

**OK**. A notification is displayed after your function app is created.

## Deploy your project to Azure

To deploy your project to Azure, follow these steps:

Select and expand the Azure icon in IntelliJ Project explorer, then select

**Deploy to Azure -> Deploy to Azure Functions**.You can select the function app from the previous section. To create a new one, select

**+**on the**Function**line. Type in the function app name and choose the proper platform. Here, you can accept the default value. Select**OK**and the new function app you created is automatically selected. Select**Run**to deploy your functions.

## Manage function apps from IDEA

To manage your function apps with **Azure Explorer** in your IDEA, follow these steps:

Select

**Function App**to see all your function apps listed.Select one of your function apps, then right-click and select

**Show Properties**to open the detail page.Right-click your

**HttpTrigger-Java**function app, then select**Trigger Function in Browser**. You should see that the browser is opened with the trigger URL.

## Add more functions to the project

To add more functions to your project, follow these steps:

Right-click the package

**org.example.functions**and select**New -> Azure Function Class**.Fill in the class name

**HttpTest**and select**HttpTrigger**in the create function class wizard, then select**OK**to create. In this way, you can create new functions as you want.

## Cleaning up functions

Select one of your function apps using **Azure Explorer** in your IDEA, then right-click and select **Delete**. This command might take several minutes to run. When it's done, the status refreshes in **Azure Explorer**.

## Next steps

You've created a Java project with an HTTP triggered function, run it on your local machine, and deployed it to Azure. Now, extend your function by continuing to the following article:
