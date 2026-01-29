---
merged_at: 2026-01-29T15:49:53.274591
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-container-apps-hosting -->

# Azure Container Apps hosting of Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on [Azure Container Apps](../container-apps/overview). Use Azure Container Apps to host your function app containers when you need to run your event-driven functions in Azure in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs. Container Apps hosting lets you run your functions in a fully managed, Kubernetes-based environment with built-in support for open-source monitoring, mTLS, Dapr, and Kubernetes Event-driven Autoscaling (KEDA).

You can write your function code in any [language stack supported by Functions](supported-languages). You can use the same Functions triggers and bindings with event-driven scaling. You can also use existing Functions client tools and the Azure portal to create containers, deploy function app containers to Container Apps, and configure continuous deployment.

Container Apps integration also means that network and observability configurations, which are defined at the Container App environment level, apply to your function app as they do to all microservices running in a Container Apps environment. You also get the other cloud-native capabilities of Container Apps, including KEDA, Dapr, Envoy. You can still use Application Insights to monitor your functions executions, and your function app can access the same virtual networking resources provided by the environment.

For a general overview of container hosting options for Azure Functions, see [Linux container support in Azure Functions](container-concepts).

## Hosting and workload profiles

There are two primary plans for Container Apps: a serverless [Consumption plan](../container-apps/plans#consumption) and a [Dedicated plan](../container-apps/plans#dedicated). Both can be used in Workload profiles environment types, with workload profiles determining the compute and memory resources available to your apps. A workload profile determines the amount of compute and memory resources available to container apps deployed in an environment. These profiles are configured to fit the different needs of your applications.

The Consumption workload profile is the default profile added to every Workload profiles environment type. You can add Dedicated workload profiles to your environment as you create an environment or after it's created. To learn more about workload profiles, see [Workload profiles in Azure Container Apps](../container-apps/workload-profiles-overview).

Container Apps hosting of containerized function apps is supported in all [regions that support Container Apps](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?products=container-apps).

If your app doesn't have specific hardware requirements, you can run your environment either in a Consumption plan or in a Dedicated plan using the default Consumption workload profile. When running functions on Container Apps, you're charged only for the Container Apps usage. For more information, see the [Azure Container Apps pricing page](https://azure.microsoft.com/pricing/details/container-apps/).

Azure Functions on Azure Container Apps supports GPU-enabled hosting in the Dedicated plan with workload profiles.

To learn how to create and deploy a function app container to Container Apps in the default Consumption plan, see [Create your first containerized functions on Azure Container Apps](functions-deploy-container-apps).

To learn how to create a Container Apps environment with workload profiles and deploy a function app container to a specific workload, see [Container Apps workload profiles](functions-how-to-custom-container#container-apps-workload-profiles).

## Functions in containers

To use Container Apps hosting, your code must run on a function app in a Linux container that you create and maintain. Functions maintains a set of [language-specific base images](https://mcr.microsoft.com/catalog?search=functions) that you can use to generate your containerized function apps.

When you create a code project using [Azure Functions Core Tools](functions-run-local) and include the [ --docker option](functions-core-tools-reference#func-init), Core Tools generates the Dockerfile with the correct base image, which you can use as a starting point when creating your container.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

When you make changes to your functions code, you must rebuild and republish your container image. For more information, see [Update an image in the registry](functions-how-to-custom-container#update-an-image-in-the-registry).

## Deployment options

Azure Functions currently supports the following methods of deploying a containerized function app to Azure Container Apps:

[Apache Maven](https://github.com/microsoft/azure-maven-plugins/wiki/Azure-Functions:-Configuration-Details#properties-for-azure-container-apps-hosting-of-azure-functions)[ARM templates](/en-us/azure/templates/microsoft.web/sites?pivots=deployment-language-arm-template)[Azure CLI](functions-deploy-container-apps)[Azure Developer CLI (azd)](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/azdtemplates)[Azure Functions Core Tools](functions-run-local#deploy-containers)[Azure Pipeline tasks](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/AzurePipelineTasks)[Azure portal](https://aka.ms/funconacablade)[Bicep files](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/Biceptemplates)[GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions)[Visual Studio Code](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/VSCode%20Sample)

You can continuously deploy your containerized apps from source code using either [Azure Pipelines](functions-how-to-azure-devops?pivots=v1#deploy-a-container) or [GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions). The continuous deployment feature of Functions isn't currently supported when deploying to Container Apps.

## Managed identity authorization

For the best security, you should connect to remote services using Microsoft Entra authentication and managed identity authorization. You can use managed identities for these connections:

When running in Container Apps, you can use Microsoft Entra ID with managed identities for all binding extensions that support managed identities. Currently, only these binding extensions support event-driven scaling when using managed identity authentication:

- Azure Event Hubs
- Azure Queue Storage
- Azure Service Bus

For other bindings, use fixed replicas when using managed identity authentication. For more information, see the [Functions developer guide](functions-reference#connections).

## Virtual network integration

When you host your function apps in a Container Apps environment, your functions are able to take advantage of both internally and externally accessible virtual networks. To learn more about environment networks, see [Networking in Azure Container Apps environment](../container-apps/networking).

## Event-driven scaling

All Functions triggers can be used in your containerized function app. However, only these triggers can dynamically scale (from zero instances) based on received events when running in a Container Apps environment:

- Azure Cosmos DB (KEDA connection)
- Azure Event Grid
- Azure Event Hubs
- Azure Blob Storage (Event Grid based)
- Azure Queue Storage
- Azure Service Bus
- Durable Functions (MSSQL storage provider)
- HTTP
- Kafka
- Timer

Azure Functions on Container Apps is designed to configure the scale parameters and rules as per the event target. You don't need to worry about configuring the KEDA scaled objects. You can still set minimum and maximum replica count when creating or modifying your function app. The following Azure CLI command sets the minimum and maximum replica count when creating a new function app in a Container Apps environment from an Azure Container Registry:

```
az functionapp create --name <APP_NAME> --resource-group <MY_RESOURCE_GROUP> --max-replicas 15 --min-replicas 1 --storage-account <STORAGE_NAME> --environment MyContainerappEnvironment --image <LOGIN_SERVER>/azurefunctionsimage:v1 --registry-username <USERNAME> --registry-password <SECURE_PASSWORD> --registry-server <LOGIN_SERVER>
```


The following command sets the same minimum and maximum replica count on an existing function app:

```
az functionapp config container set --name <APP_NAME> --resource-group <MY_RESOURCE_GROUP> --max-replicas 15 --min-replicas 1
```


## Managed resource groups

Azure Functions on Container Apps runs your containerized function app resources in specially managed resource groups. These managed resource groups help protect the consistency of your apps by preventing unintended or unauthorized modification or deletion of resources in the managed group, even by service principals.

A managed resource group is created for you the first time you create function app resources in a Container Apps environment. Container Apps resources required by your containerized function app run in this managed resource group. Any other function apps that you create in the same environment use this existing group.

A managed resource group gets removed automatically after all function app container resources are removed from the environment. While the managed resource group is visible, any attempts to modify or remove the managed resource group result in an error. To remove a managed resource group from an environment, remove all of the function app container resources and it gets removed for you.

If you run into any issues with these managed resource groups, you should contact support.

## Application logging

You can monitor your containerized function app hosted in Container Apps using Azure Monitor Application Insights in the same way you do with apps hosted by Azure Functions. For more information, see [Monitor Azure Functions](monitor-functions).

For bindings that support event-driven scaling, scale events are logged as `FunctionsScalerInfo`

and `FunctionsScalerError`

events in your Log Analytics workspace. For more information, see [Application Logging in Azure Container Apps](../container-apps/logging).

## Considerations for Container Apps hosting

Keep in mind the following considerations when deploying your function app containers to Container Apps:

- These limitations apply to Kafka triggers:
- The protocol value of
`ssl`

isn't supported when hosted on Container Apps. Use a[different protocol value](functions-bindings-kafka-trigger?pivots=programming-language-csharp#attributes). - For a Kafka trigger to dynamically scale when connected to Event Hubs, the
`username`

property must resolve to an application setting that contains the actual username value. When the default`$ConnectionString`

value is used, the Kafka trigger isn't able to cause the app to scale dynamically.

- The protocol value of
- For the built-in Container Apps
[policy definitions](../container-apps/policy-reference#policy-definitions), currently only environment-level policies apply to Azure Functions containers. - By default, a containerized function app monitors port 80 for incoming requests. If your app must use a different port, use the
to change this default port.`WEBSITES_PORT`

application setting - You aren't currently able to use built-in continuous deployment features when hosting on Container Apps. You must instead deploy from source code using either
[Azure Pipelines](functions-how-to-azure-devops?pivots=v1#deploy-a-container)or[GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions). - You currently can't move a Container Apps hosted function app deployment between resource groups or between subscriptions. Instead, you would have to recreate the existing containerized app deployment in a new resource group, subscription, or region.
- When using Container Apps, you don't have direct access to the lower-level Kubernetes APIs.
- The
`containerapp`

extension conflicts with the`appservice-kube`

extension in Azure CLI. If you have previously published apps to Azure Arc, run`az extension list`

and make sure that`appservice-kube`

isn't installed. If it is, you can remove it by running`az extension remove -n appservice-kube`

.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redisstream -->

# RedisStreamTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisStreamTrigger`

reads new entries from a stream and surfaces those elements to the function.

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Streams | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisStreamTrigger
{
internal class SimpleStreamTrigger
{
private readonly ILogger<SimpleStreamTrigger> logger;
public SimpleStreamTrigger(ILogger<SimpleStreamTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleStreamTrigger))]
public void Run(
[RedisStreamTrigger(Common.connectionStringSetting, "streamKey")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


```
package com.function.RedisStreamTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleStreamTrigger {
@FunctionName("SimpleStreamTrigger")
public void run(
@RedisStreamTrigger(
name = "req",
connection = "redisConnectionString",
key = "streamTest",
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
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
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
Write-Host ($entry | ConvertTo-Json)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

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
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
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

| Parameters | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`10`

`DeleteAfterProcess`

`false`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
`entry` |
Yes | |
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

`deleteAfterProcess`

`false`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Properties | Description | Required | Default |
|---|---|---|---|
`type` |
Yes | ||
`deleteAfterProcess` |
Optional | `false` |
|
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

`name`

`direction`

See the Example section for complete examples.

## Usage

The `RedisStreamTrigger`

Azure Function reads new entries from a stream and surfaces those entries to the function.

The trigger polls Redis at a configurable fixed interval, and uses [ XREADGROUP](https://redis.io/commands/xreadgroup/) to read elements from the stream.

The consumer group for all instances of a function is the name of the function, that is, `SimpleStreamTrigger`

for the [StreamTrigger sample](https://github.com/Azure/azure-functions-redis-extension/blob/main/samples/dotnet/RedisStreamTrigger/SimpleStreamTrigger.cs).

Each functions instance uses the [ WEBSITE_INSTANCE_ID](/en-us/azure/app-service/reference-app-settings?tabs=kudu%2Cdotnet#scaling) or generates a random GUID to use as its consumer name within the group to ensure that scaled out instances of the function don't read the same messages from the stream.

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai -->

# Azure OpenAI extension for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI extension for Azure Functions implements a set of triggers and bindings that enable you to easily integrate features and behaviors of [Azure OpenAI in Foundry Models](/en-us/azure/ai-services/openai/overview) into your function code executions.

Azure Functions is an event-driven compute service that provides a set of [triggers and bindings](functions-triggers-bindings) to easily connect with other Azure services.

With the integration between Azure OpenAI and Functions, you can build functions that can:

| Action | Trigger/binding type |
|---|---|
| Use a standard text prompt for content completion |
|

[Azure OpenAI assistant trigger](functions-bindings-openai-assistant-trigger)[Azure OpenAI assistant create output binding](functions-bindings-openai-assistantcreate-output)[Azure OpenAI assistant post input binding](functions-bindings-openai-assistantpost-input)[Azure OpenAI assistant query input binding](functions-bindings-openai-assistantquery-input)[Azure OpenAI embeddings input binding](functions-bindings-openai-embeddings-input)[Azure OpenAI embeddings store output binding](functions-bindings-openai-embeddingsstore-output)[Azure OpenAI semantic search input binding](functions-bindings-openai-semanticsearch-input)## Install extension

The extension NuGet package you install depends on the C# mode [in-process](functions-dotnet-class-library) or [isolated worker process](dotnet-isolated-process-guide) you're using in your function app:

Add the Azure OpenAI extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.OpenAI](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI) NuGet package, which you can do using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.OpenAI --prerelease
```


When using a vector database for storing content, you should also install at least one of these NuGet packages:

- Azure AI Search:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.AzureAISearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.AzureAISearch) - Azure Cosmos DB for MongoDB vCore:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch) - Azure Cosmos DB for NoSQL:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBNoSQLSearch) - Azure Data Explorer:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.Kusto](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.Kusto)

## Install bundle

To be able to use this preview binding extension in your app, you must reference a preview extension bundle that includes it.

Add or replace the following code in your `host.json`

file, which specifically targets the latest [preview version of the 4.x bundle](https://github.com/Azure/azure-functions-extension-bundles/releases?q=preview+NOT+experimental&expanded=true):

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.0.0, 5.0.0)"
}
}
```


Select the previous link to verify that the latest preview bundle version does contain the preview extension.

## Connecting to OpenAI

To use the Azure OpenAI binding extension, you need to specify a connection to OpenAI. This connection is defined using application settings, and the `AIConnectionName`

property of the trigger or binding. You can also use environment variables to define key-based connections.

We recommend that you use managed identity-based connections and the `AIConnectionName`

property.

The OpenAI bindings have an `AIConnectionName`

property that you can use to specify the `<ConnectionNamePrefix>`

for this group of app settings that define the connection to Azure OpenAI:

| Setting name | Description |
|---|---|
`<CONNECTION_NAME_PREFIX>__endpoint` |
Sets the URI endpoint of the Azure OpenAI in Foundry Models. This setting is always required. |
`<CONNECTION_NAME_PREFIX>__clientId` |
Sets the specific user-assigned identity to use when obtaining an access token. Requires that `<CONNECTION_NAME_PREFIX>__credential` is set to `managedidentity` . The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in
`credential` shouldn't be set. |
`<CONNECTION_NAME_PREFIX>__credential` |
Defines how an access token is obtained for the connection. Use `managedidentity` for managed identity authentication. This value is only valid when a managed identity is available in the hosting environment. |
`<CONNECTION_NAME_PREFIX>__managedIdentityResourceId` |
When `credential` is set to `managedidentity` , this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in
`credential` shouldn't be set. |
`<CONNECTION_NAME_PREFIX>__key` |
Sets the shared secret key required to access the endpoint of Azure OpenAI using key-based authentication. As a security best practice, you should always use Microsoft Entra ID with managed identities for authentication. |

Consider these managed identity connection settings when then `AIConnectionName`

property is set to `myAzureOpenAI`

:

`myAzureOpenAI__endpoint=https://contoso.openai.azure.com/`

`myAzureOpenAI__credential=managedidentity`

`myAzureOpenAI__clientId=aaaaaaaa-bbbb-cccc-1111-222222222222`


At runtime, these settings are collectively interpreted by the host as a single `myAzureOpenAI`

setting like this:

```
"myAzureOpenAI":
{
"endpoint": "https://contoso.openai.azure.com/",
"credential": "managedidentity",
"clientId": "aaaaaaaa-bbbb-cccc-1111-222222222222"
}
```


When using managed identities, make sure to add your identity to the [Cognitive Services OpenAI User](../role-based-access-control/built-in-roles/ai-machine-learning#cognitive-services-openai-user) role.

When running locally, you must add these settings to the *local.settings.json* project file. For more information, see [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

For more information, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/language-support-policy -->

# Azure Functions language stack support policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the support policy for the language stacks supported by Azure Functions. Guidance is language-specific. Make sure to choose your preferred development language at the [top of the article](#top).

## Retirement process

The Functions runtime includes the Functions host and programming language-specific workers. To maintain full-support coverage when running your functions in Azure, Functions support aligns with end-of-life support for a given language. To help you keep your apps up-to-date and supported, Functions implements a phased reduction in support as language stack versions reach their end-of-life dates. Support ends on the earlier of: the community end-of-support date for the language or the end-of-support date for the underlying base operating system. Retirement dates are published at general availability (GA) to allow time for upgrade planning and testing.

**Notification phase**:The Functions team sends you notification emails about upcoming language version retirements that affect your function apps. When you receive this notification, you should prepare to upgrade these apps to use to a supported version.

**Retirement phase**:After the language end-of-life date, function apps that use retired language versions can still be created and deployed, and they continue to run on the platform. However, these apps aren't eligible for new features, security patches, and performance optimizations until after you upgrade them to a supported language version. Further, if required, in certain cases we will limit the number of instances allocated to these apps including limit scaling to 1 instance.

Important

If you're running function apps using an unsupported runtime or language version, you might encounter issues and performance implications and are required to upgrade before receiving support for your function app. As such, you're highly encouraged to upgrade the language version of such an app to a supported version. TO learn how, see

[Update language stack versions in Azure Functions](update-language-versions).

## Retirement policy exceptions

Any Functions-supported exceptions to language-specific retirement policies are documented here:

There are currently no exceptions to the general retirement policy.


## Language support-related resources

Use these resources to better understand and plan for language support-related changes in your function apps.

| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[.NET support policy page](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)**Configuring language versions**[Isolated worker model](dotnet-isolated-process-guide#supported-versions)[In-process model](functions-dotnet-class-library#supported-versions)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Node.js release page on GitHub](https://github.com/nodejs/Release#release-schedule)**Configuring language versions**[Setting the Node version](functions-reference-node#setting-the-node-version)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Node.js release page on GitHub](https://github.com/nodejs/Release#release-schedule)**Configuring language versions**[Setting the Node version](functions-reference-node#setting-the-node-version)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Java support on Azure and Azure Stack](/en-us/azure/developer/java/fundamentals/java-support-on-azure)**Configuring language versions**[Update the stack configuration](update-language-versions#update-the-stack-configuration)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[PowerShell Support Lifecycle](/en-us/powershell/scripting/powershell-support-lifecycle#powershell-end-of-support-dates)**Configuring language versions**[Changing the PowerShell version](functions-reference-python#supported-python-versions)| Resource | Details |
|---|---|
Supported versions |
|

**Language version support timelines**[Python developer's guide](https://devguide.python.org/#status-of-python-branches)**Configuring language versions**[Changing Python version](set-runtime-version?tabs=azure-portal&pivots=platform-linux#manual-version-updates-on-linux)## Frequently asked questions

This section provides you with answers to questions that are frequently asked about language support policies.

### Which versions of my preferred language does Functions currently support?

For the up-to-date list of supported language stack versions, see [Supported languages in Azure Functions](supported-languages#languages-by-runtime-version).

### How long will Functions continue to support my language version?

Support ends on the earlier of: the community end-of-support date for the language or the end-of-support date for the underlying base operating system. Retirement dates are published at general availability (GA) to allow time for upgrade planning and testing. For the expected end-of-life dates of currently supported versions, see [Supported languages in Azure Functions](supported-languages#languages-by-runtime-version).

### What happens when my runtime version reaches the end of support?

After a previously supported Functions runtime version reaches its end-of-support, Microsoft no longer provides bug fixes, security updates, or patches. Apps using retired versions may also face performance degradation. You must upgrade to a supported version to maintain security and stability.

### Can I continue to use an unsupported language stack or runtime version?

You can continue to use previously supported language stacks and Functions runtime versions beyond the end-of-support date. However, you must take into account that unsupported runtime versions don't receive updates, security patches, or official support from Microsoft. Your apps might also face performance degradation when using retired runtime versions.

### How do I upgrade my function app to a newer supported language stack or runtime version?

To make sure that your app is compatible with both the latest supported Functions runtime version and the latest version of your language stack, see [Update language stack versions in Azure Functions](update-language-versions)

### How do I check which language stack and runtime version is being used by my function app?

Azure provides these methods to check the current runtime version used by your function app:

The language stack used by your function app is determined based on the value of the `FUNCTIONS_WORKER_RUNTIME`

application setting. For more information, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## Related articles

To learn more about how to upgrade your function app's language version, see these articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/manage-connections -->

# Manage connections in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Functions in a function app share resources. Among those shared resources are connections: HTTP connections, database connections, and connections to services such as Azure Storage. When many functions are running concurrently in a Consumption plan, it's possible to run out of available connections. This article explains how to code your functions to avoid using more connections than they need.

Note

Connection limits described in this article apply only when running in a [Consumption plan](consumption-plan). However, the techniques described here may be beneficial when running on any plan.

## Connection limit

The number of available connections in a Consumption plan is limited partly because a function app in this plan runs in a [sandbox environment](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox). One of the restrictions that the sandbox imposes on your code is a limit on the number of outbound connections, which is currently 600 active (1,200 total) connections per instance. When you reach this limit, the functions runtime writes the following message to the logs: `Host thresholds exceeded: Connections`

. For more information, see the [Functions service limits](functions-scale#service-limits).

This limit is per instance. When the [scale controller adds function app instances](event-driven-scaling) to handle more requests, each instance has an independent connection limit. That means there's no global connection limit, and you can have much more than 600 active connections across all active instances.

When troubleshooting, make sure that you have enabled Application Insights for your function app. Application Insights lets you view metrics for your function apps like executions. For more information, see [View telemetry in Application Insights](analyze-telemetry-data#view-telemetry-in-application-insights).

## Static clients

To avoid holding more connections than necessary, reuse client instances rather than creating new ones with each function invocation. We recommend reusing client connections for any language that you might write your function in. For example, .NET clients like the [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true), [DocumentClient](/en-us/dotnet/api/microsoft.azure.documents.client.documentclient), and Azure Storage clients can manage connections if you use a single, static client.

Here are some guidelines to follow when you're using a service-specific client in an Azure Functions application:

*Do not*create a new client with every function invocation.*Do*create a single, static client that every function invocation can use.*Consider*creating a single, static client in a shared helper class if different functions use the same service.

## Client code examples

This section demonstrates best practices for creating and using clients from your function code.

### HTTP requests

Here's an example of C# function code that creates a static [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true) instance:

```
// Create a single, static HttpClient
private static HttpClient httpClient = new HttpClient();
public static async Task Run(string input)
{
var response = await httpClient.GetAsync("https://example.com");
// Rest of function
}
```


A common question about [HttpClient](/en-us/dotnet/api/system.net.http.httpclient?view=netcore-3.1&preserve-view=true) in .NET is "Should I dispose of my client?" In general, you dispose of objects that implement `IDisposable`

when you're done using them. But you don't dispose of a static client because you aren't done using it when the function ends. You want the static client to live for the duration of your application.

### Azure Cosmos DB clients

[CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) connects to an Azure Cosmos DB instance. The Azure Cosmos DB documentation recommends that you [use a singleton Azure Cosmos DB client for the lifetime of your application](/en-us/azure/cosmos-db/performance-tips-dotnet-sdk-v3-sql#sdk-usage). The following example shows one pattern for doing that in a function:

```
#r "Microsoft.Azure.Cosmos"
using Microsoft.Azure.Cosmos;
private static Lazy<CosmosClient> lazyClient = new Lazy<CosmosClient>(InitializeCosmosClient);
private static CosmosClient cosmosClient => lazyClient.Value;
private static CosmosClient InitializeCosmosClient()
{
// Perform any initialization here
var uri = "https://youraccount.documents.azure.com:443";
var authKey = "authKey";
return new CosmosClient(uri, authKey);
}
public static async Task Run(string input)
{
Container container = cosmosClient.GetContainer("database", "collection");
MyItem item = new MyItem{ id = "myId", partitionKey = "myPartitionKey", data = "example" };
await container.UpsertItemAsync(document);
// Rest of function
}
```


Also, create a file named "function.proj" for your trigger and add the below content :

```
<Project Sdk="Microsoft.NET.Sdk">
<PropertyGroup>
<TargetFramework>netcoreapp3.1</TargetFramework>
</PropertyGroup>
<ItemGroup>
<PackageReference Include="Microsoft.Azure.Cosmos" Version="3.23.0" />
</ItemGroup>
</Project>
```


## SqlClient connections

Your function code can use the .NET Framework Data Provider for SQL Server ([SqlClient](/en-us/dotnet/api/system.data.sqlclient)) to make connections to a SQL relational database. This is also the underlying provider for data frameworks that rely on ADO.NET, such as [Entity Framework](/en-us/ef/ef6/). Unlike [HttpClient](/en-us/dotnet/api/system.net.http.httpclient) and [DocumentClient](/en-us/dotnet/api/microsoft.azure.documents.client.documentclient) connections, ADO.NET implements connection pooling by default. But because you can still run out of connections, you should optimize connections to the database. For more information, see [SQL Server Connection Pooling (ADO.NET)](/en-us/dotnet/framework/data/adonet/sql-server-connection-pooling).

Tip

Some data frameworks, such as Entity Framework, typically get connection strings from the **ConnectionStrings** section of a configuration file. In this case, you must explicitly add SQL database connection strings to the **Connection strings** collection of your function app settings and in the [local.settings.json file](functions-develop-local#local-settings-file) in your local project. If you're creating an instance of [SqlConnection](/en-us/dotnet/api/system.data.sqlclient.sqlconnection) in your function code, you should store the connection string value in **Application settings** with your other connections.

## Next steps

For more information about why we recommend static clients, see [Improper instantiation antipattern](/en-us/azure/architecture/antipatterns/improper-instantiation/).

For more Azure Functions performance tips, see [Optimize the performance and reliability of Azure Functions](functions-best-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-nat-gateway -->

# Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual network address translation (NAT) simplifies outbound-only internet connectivity for virtual networks. When configured on a subnet, all outbound connectivity uses your specified static public IP addresses. An NAT can be useful for apps that need to consume a third-party service that uses an allowlist of IP address as a security measure. To learn more, see [What is Azure NAT Gateway?](../virtual-network/nat-gateway/nat-overview).

This tutorial shows you how to use NAT gateways to route outbound traffic from an HTTP triggered function. This function lets you check its own outbound IP address. During this tutorial, you'll:

- Create a virtual network
- Create a Premium plan function app
- Create a public IP address
- Create a NAT gateway
- Configure function app to route outbound traffic through the NAT gateway

Note

You can't use a NAT gateway to route outbound traffic to an Azure Storage account in the same region as your function app. Services deployed in the same region your storage account use private Azure IP addresses for communication. For more information, see [NAT Gateway frequenty asked questions](/en-us/azure/nat-gateway/faq#can-i-use-nat-gateway-to-connect-to-a-storage-account-public-endpoint-in-the-same-region).

## Topology

The following diagram shows the architecture of the solution that you create:

Functions running in the Premium plan have the same hosting capabilities as web apps in Azure App Service, which includes the VNet Integration feature. To learn more about VNet Integration, including troubleshooting and advanced configuration, see [Integrate your app with an Azure virtual network](../app-service/overview-vnet-integration).

## Prerequisites

For this tutorial, it's important that you understand IP addressing and subnetting. You can start with [this article that covers the basics of addressing and subnetting](https://support.microsoft.com/help/164015/understanding-tcp-ip-addressing-and-subnetting-basics). Many more articles and videos are available online.

If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

If you've already completed the [integrate Functions with an Azure virtual network](functions-create-vnet) tutorial, you can skip to [Create an HTTP trigger function](#create-function).

## Create a virtual network

From the Azure portal menu, select

**Create a resource**. From the Azure Marketplace, select**Networking**>**Virtual network**.In

**Create virtual network**, enter or select the settings specified as shown in the following table:Setting Value Subscription Select your subscription. Resource group Select **Create new**, enter*myResourceGroup*, then select**OK**.Name Enter *myResourceGroup-vnet*.Location Select **East US**.Select

**Next: IP Addresses**, and for**IPv4 address space**, enter*10.10.0.0/16*.Select

**Add subnet**, then enter*Tutorial-Net*for**Subnet name**and*10.10.1.0/24*for**Subnet address range**.Select

**Add**, then select**Review + create**. Leave the rest as default and select**Create**.In

**Create virtual network**, select**Create**.

Next, you create a function app in the [Premium plan](functions-premium-plan). This plan provides serverless scale while supporting virtual network integration.

## Create a function app in a Premium plan

This tutorial shows you how to create your function app in a [Premium plan](functions-premium-plan). The same functionality is also available when you host your app in a [Flex Consumption plan](flex-consumption-plan) or in a [Dedicated (App Service) plan](dedicated-plan).

Note

For the best experience in this tutorial, choose .NET for runtime stack and choose Windows for operating system. Also, create your function app in the same region as your virtual network.

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Compute**>**Function App**.Under

**Select a hosting option**, select**Functions Premium**>**Select**to create your app in a[Premium plan](functions-premium-plan). In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run. To learn more about different hosting plans, see[Overview of plans](functions-scale#overview-of-plans).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which this new function app is created. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which to create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Do you want to deploy code or container image?**Code Option to publish code files or a Docker container. **Operating system**Preferred OS Choose either Linux or Windows. **Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. **Version**Supported language version Choose a supported version of your function programming language. **Region**Preferred region Choose a [region](https://azure.microsoft.com/regions/)near you or near other services your functions access.Under

**Environment details**for either**Windows Plan**or**Linux Plan**, select**Create new**,**Name**your App Service plan, and select a**Pricing plan**. The default pricing plan is**EP1**, where EP stands for*elastic premium*. To learn more, see the[list of Premium SKUs](functions-premium-plan#available-instance-skus). When running JavaScript functions on a Premium plan, you should choose an instance that has fewer vCPUs. For more information, see[Choose single-core Premium plans](functions-reference-node#considerations-for-javascript-functions).Unless you want to enable

, keep the default value of**Zone Redundancy****Disabled**.Select

**Next: Storage**. On the**Storage**page, create the default host[storage account](../storage/common/storage-account-create)required by your function app. Storage account names must be between 3 and 24 characters in length and only can contain numbers and lowercase letters. You can also use an existing account, which must meet the[storage account requirements](storage-considerations#storage-account-requirements).Unless you're enabling virtual network integration, select

**Next: Monitoring**to skip the**Networking**tab. On the**Monitoring**page, enter the following settings:Setting Suggested value Description Enable Application Insights Yes Enables built-in Application Insight integration for monitoring your functions code. [Application Insights](functions-monitoring)Default Creates an Application Insights resource of the same *App name*in the nearest supported region. By expanding this setting, you can change the**New resource name**or choose a different**Location**in an[Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/)to store your data.Select

**Review + create**to accept the defaults for the remaining pages and review the app configuration selections.On the

**Review + create**page, review your settings, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

## Connect your function app to the virtual network

You can now connect your function app to the virtual network.

In your function app, select

**Networking**in the left menu, then under**VNet Integration**, select**Click here to configure**.On the

**VNET Integration**page, select**Add VNet**.In

**Network Feature Status**, use the settings in the table below the image:Setting Suggested value Description **Virtual Network**MyResourceGroup-vnet This virtual network is the one you created earlier. **Subnet**Create New Subnet Create a subnet in the virtual network for your function app to use. VNet Integration must be configured to use an empty subnet. **Subnet name**Function-Net Name of the new subnet. **Virtual network address block**10.10.0.0/16 You should only have one address block defined. **Subnet Address Block**10.10.2.0/24 The subnet size restricts the total number of instances that your Premium plan function app can scale out to. This example uses a `/24`

subnet with 254 available host addresses. This subnet is over-provisioned, but easy to calculate.Select

**OK**to add the subnet. Close the**VNet Integration**and**Network Feature Status**pages to return to your function app page.

The function app can now access the virtual network. When connectivity is enabled, the [ vnetrouteallenabled](functions-app-settings#vnetrouteallenabled) site setting is set to

`1`

. You must have either this site setting or the legacy [application setting set to](functions-app-settings#website_vnet_route_all)

`WEBSITE_VNET_ROUTE_ALL`

`1`

.Next, you'll add an HTTP-triggered function to the function app.

## Create an HTTP trigger function

From the left menu of the

**Functions**window, select**Functions**, then select**Add**from the top menu.From the

**New Function**window, select**Http trigger**and accept the default name for**New Function**, or enter a new name.In

**Code + Test**, replace the template-generated C# script (.csx) code with the following code:`#r "Newtonsoft.Json" using System.Net; using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Primitives; using Newtonsoft.Json; public static async Task<IActionResult> Run(HttpRequest req, ILogger log) { log.LogInformation("C# HTTP trigger function processed a request."); var client = new HttpClient(); var response = await client.GetAsync(@"https://ifconfig.me"); var responseMessage = await response.Content.ReadAsStringAsync(); return new OkObjectResult(responseMessage); }`

This code calls an external website that returns the IP address of the caller, which in this case is this function. This method lets you easily determine the outbound IP address being used by your function app.


Now you're ready to run the function and check the current outbound IPs.

## Verify current outbound IPs

Now, you can run the function. But first, check in the portal and see what outbound IPs are being use by the function app.

In your function app, select

**Properties**and review the**Outbound IP Addresses**field.Now, return to your HTTP trigger function, select

**Code + Test**and then**Test/Run**.Select

**Run**to execute the function, then switch to the**Output**and verify that IP address in the HTTP response body is one of the values from the outbound IP addresses you viewed earlier.

Now, you can create a public IP and use a NAT gateway to modify this outbound IP address.

## Create public IP

From your resource group, select

**Add**, search the Azure Marketplace for**Public IP address**, and select**Create**. Use the settings in the table below the image:Setting Suggested value **IP Version**IPv4 **SKU**Standard **Tier**Regional **Name**Outbound-IP **Subscription**ensure your subscription is displayed **Resource group**myResourceGroup (or name you assigned to your resource group) **Location**East US (or location you assigned to your other resources) **Availability Zone**No Zone Select

**Create**to submit the deployment.Once the deployment completes, navigate to your newly created Public IP Address resource and view the IP Address in the

**Overview**.

## Create NAT gateway

Now, let's create the NAT gateway. When you start with the [previous virtual networking tutorial](functions-create-vnet), `Function-Net`

was the suggested subnet name and `MyResourceGroup-vnet`

was the suggested virtual network name in that tutorial.

From your resource group, select

**Add**, search the Azure Marketplace for**NAT gateway**, and select**Create**. Use the settings in the table below the image to populate the**Basics**tab:Setting Suggested value **Subscription**Your subscription **Resource group**myResourceGroup (or name you assigned to your resource group) **NAT gateway name**myNatGateway **Region**East US (or location you assigned to your other resources) **Availability Zone**None Select

**Next: Outbound IP**. In the**Public IP addresses**field, select the previously created public IP address. Leave**Public IP Prefixes**unselected.Select

**Next: Subnet**. Select the*myResourceGroup-vnet*resource in the**Virtual network**field and*Function-Net*subnet.Select

**Review + Create**then**Create**to submit the deployment.

Once the deployment completes, the NAT gateway is ready to route traffic from your function app subnet to the Internet.

## Verify new outbound IPs

Repeat [the steps earlier](#verify-current-outbound-ips) to run the function again. You should now see the outbound IP address that you configured in the NAT shown in the function output.

## Clean up resources

You created resources to complete this tutorial. You'll be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). To avoid incurring extra costs, delete the resources when you know longer need them.

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-java -->

# Azure Functions Java developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide contains detailed information to help you succeed developing Azure Functions using Java.

As a Java developer, if you're new to Azure Functions, consider first reading one of the following articles:

| Getting started | Concepts | Scenarios/samples |
|---|---|---|

## Java function basics

A Java function is a `public`

method, decorated with the annotation `@FunctionName`

. This method defines the entry for a Java function, and must be unique in a particular package. The package can have multiple classes with multiple public methods annotated with `@FunctionName`

. A single package is deployed to a function app in Azure. In Azure, the function app provides the deployment, execution, and management context for your individual Java functions.

## Programming model

The concepts of [triggers and bindings](functions-triggers-bindings) are fundamental to Azure Functions. Triggers start the execution of your code. Bindings give you a way to pass data to and return data from a function, without having to write custom data access code.

## Create Java functions

To make it easier to create Java functions, there are Maven-based tooling and archetypes that use predefined Java templates to help you create projects with a specific function trigger.

### Maven-based tooling

The following developer environments have Azure Functions tooling that lets you create Java function projects:

These articles show you how to create your first functions using your IDE of choice.

### Project scaffolding

If you prefer command line development from the Terminal, the simplest way to scaffold Java-based function projects is to use `Apache Maven`

archetypes. The Java Maven archetype for Azure Functions is published under the following *groupId*:*artifactId*: [com.microsoft.azure:azure-functions-archetype](https://search.maven.org/artifact/com.microsoft.azure/azure-functions-archetype/).

The following command generates a new Java function project using this archetype:

```
mvn archetype:generate \
-DarchetypeGroupId=com.microsoft.azure \
-DarchetypeArtifactId=azure-functions-archetype
```


To get started using this archetype, see the [Java quickstart](how-to-create-function-azure-cli?pivots=programming-language-java).

## Folder structure

Here's the folder structure of an Azure Functions Java project:

```
FunctionsProject
| - src
| | - main
| | | - java
| | | | - FunctionApp
| | | | | - MyFirstFunction.java
| | | | | - MySecondFunction.java
| - target
| | - azure-functions
| | | - FunctionApp
| | | | - FunctionApp.jar
| | | | - host.json
| | | | - MyFirstFunction
| | | | | - function.json
| | | | - MySecondFunction
| | | | | - function.json
| | | | - bin
| | | | - lib
| - pom.xml
```


You can use a shared [host.json](functions-host-json) file to configure the function app. Each function has its own code file (.java) and binding configuration file (function.json).

You can have more than one function in a project. However, don't put your functions into separate jars. Using multiple jars in a single function app isn't supported. The `FunctionApp`

in the target directory is what gets deployed to your function app in Azure.

## Triggers and annotations

Functions are invoked by a trigger, such as an HTTP request, a timer, or an update to data. Your function needs to process that trigger, and any other inputs, to produce one or more outputs.

Use the Java annotations included in the [com.microsoft.azure.functions.annotation.*](/en-us/java/api/com.microsoft.azure.functions.annotation) package to bind input and outputs to your methods. For more information, see the [Java reference docs](/en-us/java/api/com.microsoft.azure.functions.annotation).

Important

You must configure an Azure Storage account in your [local.settings.json](functions-develop-local#local-settings-file) to run Azure Blob storage, Azure Queue storage, or Azure Table storage triggers locally.

Example:

```
public class Function {
public String echo(@HttpTrigger(name = "req",
methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
String req, ExecutionContext context) {
return String.format(req);
}
}
```


Here's the generated corresponding `function.json`

by the [azure-functions-maven-plugin](https://mvnrepository.com/artifact/com.microsoft.azure/azure-functions-maven-plugin):

```
{
"scriptFile": "azure-functions-example.jar",
"entryPoint": "com.example.Function.echo",
"bindings": [
{
"type": "httpTrigger",
"name": "req",
"direction": "in",
"authLevel": "anonymous",
"methods": [ "GET","POST" ]
},
{
"type": "http",
"name": "$return",
"direction": "out"
}
]
}
```


## Java versions

The version of Java on which your app runs in Azure is specified in the pom.xml file. The Maven archetype currently generates a pom.xml for Java 8, which you can change before publishing. The Java version in pom.xml should match the version of Java on which you develop and test your app locally.

### Supported versions

The following table shows current supported Java versions for each major version of the Functions runtime, by operating system:

| Functions version | Java versions (Windows) | Java versions (Linux) |
|---|---|---|
| 4.x | 21 17 11 8 |
21 17 11 8 |
| 3.x | 11 8 |
11 8 |
| 2.x | 8 | n/a |

Unless you specify a Java version for your deployment, the Maven archetype defaults to Java 8 during deployment to Azure.

### Specify the deployment version

You can control the version of Java targeted by the Maven archetype by using the `-DjavaVersion`

parameter. This parameter must match [supported Java versions](supported-languages?pivots=programming-language-java#languages-by-runtime-version).

The Maven archetype generates a pom.xml that targets the specified Java version. The following elements in pom.xml indicate the Java version to use:

| Element | Java 8 value | Java 11 value | Java 17 value | Java 21 value | Description |
|---|---|---|---|---|---|
`Java.version` |
1.8 | 11 | 17 | 21 | Version of Java used by the maven-compiler-plugin. |
`JavaVersion` |
8 | 11 | 17 | 21 | Java version hosted by the function app in Azure. |

The following examples show the settings for Java 8 in the relevant sections of the pom.xml file:

`Java.version`


```
<properties>
<project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
<java.version>1.8</java.version>
<azure.functions.maven.plugin.version>1.6.0</azure.functions.maven.plugin.version>
<azure.functions.java.library.version>1.3.1</azure.functions.java.library.version>
<functionAppName>fabrikam-functions-20200718015742191</functionAppName>
<stagingDirectory>${project.build.directory}/azure-functions/${functionAppName}</stagingDirectory>
</properties>
```


`JavaVersion`


```
<runtime>
<!-- runtime os, could be windows, linux or docker-->
<os>windows</os>
<javaVersion>8</javaVersion>
<!-- for docker function, please set the following parameters -->
<!-- <image>[hub-user/]repo-name[:tag]</image> -->
<!-- <serverId></serverId> -->
<!-- <registryUrl></registryUrl> -->
</runtime>
```


Important

You must have the JAVA_HOME environment variable set correctly to the JDK directory that is used during code compiling using Maven. Make sure that the version of the JDK is at least as high as the `Java.version`

setting.

### Specify the deployment OS

Maven also lets you specify the operating system on which your function app runs in Azure. Use the `os`

element to choose the operating system.

| Element | Windows | Linux | Docker |
|---|---|---|---|
`os` |
`windows` |
`linux` |
`docker` |

The following example shows the operating system setting in the `runtime`

section of the pom.xml file:

```
<runtime>
<!-- runtime os, could be windows, linux or docker-->
<os>windows</os>
<javaVersion>8</javaVersion>
<!-- for docker function, please set the following parameters -->
<!-- <image>[hub-user/]repo-name[:tag]</image> -->
<!-- <serverId></serverId> -->
<!-- <registryUrl></registryUrl> -->
</runtime>
```


## JDK runtime availability and support

Microsoft and [Adoptium](https://adoptium.net/) builds of OpenJDK are provided and supported on Functions for Java 8 (Adoptium), Java 11, 17 and 21 (MSFT). These binaries are provided as a no-cost, multi-platform, production-ready distribution of the OpenJDK for Azure. They contain all the components for building and running Java SE applications.

For local development or testing, you can download the [Microsoft build of OpenJDK](/en-us/java/openjdk/download) or [Adoptium Temurin](https://adoptium.net/?variant=openjdk8&jvmVariant=hotspot) binaries for free. [Azure support](https://azure.microsoft.com/support/) for issues with the JDKs and function apps is available with a [qualified support plan](https://azure.microsoft.com/support/plans/).

If you would like to continue using the Zulu for Azure binaries on your Function app, [configure your app accordingly](https://github.com/Azure/azure-functions-java-worker/wiki/Customize-JVM-to-use-Zulu). You can continue to use the Azul binaries for your site. However, any security patches or improvements are only available in new versions of the OpenJDK. Because of this, you should eventually remove this configuration so that your apps use the latest available version of Java.

## Customize JVM

Functions lets you customize the Java virtual machine (JVM) used to run your Java functions. The [following JVM options](https://github.com/Azure/azure-functions-java-worker/blob/master/worker.config.json#L7) are used by default:

`-XX:+TieredCompilation`

`-XX:TieredStopAtLevel=1`

`-noverify`

`-Djava.net.preferIPv4Stack=true`

`-jar`


You can provide other arguments to the JVM by using one of the following application settings, depending on the plan type:

| Plan type | Setting name | Comment |
|---|---|---|
|

`languageWorkers__java__arguments`

[Premium plan](functions-premium-plan)[Dedicated plan](dedicated-plan)`JAVA_OPTS`

The following sections show you how to add these settings. To learn more about working with application settings, see the [Work with application settings](functions-how-to-use-azure-function-app-settings#settings) section.

### Azure portal

In the [Azure portal](https://portal.azure.com), use the [Application Settings tab](functions-how-to-use-azure-function-app-settings#settings) to add either the `languageWorkers__java__arguments`

or the `JAVA_OPTS`

setting.

### Azure CLI

You can use the [az functionapp config appsettings set](/en-us/cli/azure/functionapp/config/appsettings) command to add these settings, as shown in the following example for the `-Djava.awt.headless=true`

option:

```
az functionapp config appsettings set \
--settings "languageWorkers__java__arguments=-Djava.awt.headless=true" \
--name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


This example enables headless mode. Replace `<APP_NAME>`

with the name of your function app, and `<RESOURCE_GROUP>`

with the resource group.

## Third-party libraries

Azure Functions supports the use of third-party libraries. By default, all dependencies specified in your project `pom.xml`

file are automatically bundled during the [ mvn package](https://github.com/Microsoft/azure-maven-plugins/blob/master/azure-functions-maven-plugin/README.md#azure-functionspackage) goal. For libraries not specified as dependencies in the

`pom.xml`

file, place them in a `lib`

directory in the function's root directory. Dependencies placed in the `lib`

directory are added to the system class loader at runtime.The `com.microsoft.azure.functions:azure-functions-java-library`

dependency is provided on the classpath by default, and doesn't need to be included in the `lib`

directory. Also, [azure-functions-java-worker](https://github.com/Azure/azure-functions-java-worker) adds dependencies listed [here](https://github.com/Azure/azure-functions-java-worker/wiki/Azure-Java-Functions-Worker-Dependencies) to the classpath.

## Data type support

You can use plain-old Java objects (POJOs), types defined in `azure-functions-java-library`

, or primitive data types such as `String`

and `Integer`

to bind to input or output bindings.

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

### POJOs

For converting input data to POJO, [azure-functions-java-worker](https://github.com/Azure/azure-functions-java-worker) uses the [gson](https://github.com/google/gson) library. POJO types used as inputs to functions should be `public`

.

### Binary data

Bind binary inputs or outputs to `byte[]`

, by setting the `dataType`

field in your function.json to `binary`

:

```
@FunctionName("BlobTrigger")
@StorageAccount("AzureWebJobsStorage")
public void blobTrigger(
@BlobTrigger(name = "content", path = "myblob/{fileName}", dataType = "binary") byte[] content,
@BindingName("fileName") String fileName,
final ExecutionContext context
) {
context.getLogger().info("Java Blob trigger function processed a blob.\n Name: " + fileName + "\n Size: " + content.length + " Bytes");
}
```


If you expect null values, use `Optional<T>`

.

### SDK types (preview)

You can currently use these Blob Storage SDK types in your bindings: `BlobClient`

and `BlobContainerClient`

.

With SDK types support enabled, your functions can use Azure SDK client types to access blobs as streams directly from storage, which provides these benefits over POJOs or binary types:

- Lower latency
- Reduced memory requirements
- Removes request-based size limits (uses service defaults)
- Provides access to the full SDK surface: metadata, ACLs, legal holds, and other SDK-specific data.

#### Requirements

- Set the
app setting to`JAVA_ENABLE_SDK_TYPES`

`true`

to enable SDK types. `azure-functions-maven-plugin`

(or Gradle plug-in) version`1.38.0`

or a higher version.

#### Examples

Blob trigger that uses `BlobClient`

to access properties of the blob.

```
@FunctionName("processBlob")
public void run(
@BlobTrigger(
name = "content",
path = "images/{name}",
connection = "AzureWebJobsStorage") BlobClient blob,
@BindingName("name") String file,
ExecutionContext ctx)
{
ctx.getLogger().info("Size = " + blob.getProperties().getBlobSize());
}
```


Blob trigger that uses `BlobContainerClient`

to access info about blobs in the container.

```
@FunctionName("containerOps")
public void run(
@BlobTrigger(
name = "content",
path = "images/{name}",
connection = "AzureWebJobsStorage") BlobContainerClient container,
ExecutionContext ctx)
{
container.listBlobs()
.forEach(b -> ctx.getLogger().info(b.getName()));
}
```


Blob input binding that uses `BlobClient`

to get information about the blob that triggered the execution.

```
@FunctionName("checkAgainstInputBlob")
public void run(
@BlobInput(
name = "inputBlob",
path = "inputContainer/input.txt") BlobClient inputBlob,
@BlobTrigger(
name = "content",
path = "images/{name}",
connection = "AzureWebJobsStorage",
dataType = "string") String triggerBlob,
ExecutionContext ctx)
{
ctx.getLogger().info("Size = " + inputBlob.getProperties().getBlobSize());
}
```


#### Considerations

- The
`dataType`

setting on`@BlobTrigger`

is ignored when binding to an SDK type. - Currently, only one SDK type can be used at a time in a given function definition. When a function has both a Blog trigger or input binding and a Blob output binding, one binding can use an SDK type (such as
`BlobClient`

) and the others must use a native type or POJO. - You can use managed identities with SDK types.

#### Troubleshooting

These are potential errors that might occur when using SDK types:

| Exception | Meaning |
|---|---|
`SdkAnalysisException` |
Build plug-in couldn’t create metadata. This might be due to duplicate SDK-types in a single function definition, an unsupported parameter type, or some other misconfiguration. |
`SdkRegistryException` |
Runtime doesn’t recognize the stored FQCN, which can be caused by mismatched library versions. |
`SdkHydrationException` |
Middleware failed to build the SDK client, which can occur due to missing environment variables, reflection errors, credential failures, and similar runtime issues. |
`SdkTypeCreationException` |
Factory couldn’t turn metadata into the final SDK type, which is usually caused by a casting issues. |

Check the inner message for more details about the exact cause. Most SDK types issues are caused by misspelled environment variable names or missing dependencies.

## Bindings

Input and output bindings provide a declarative way to connect to data from within your code. A function can have multiple input and output bindings.

### Input binding example

```
package com.example;
import com.microsoft.azure.functions.annotation.*;
public class Function {
@FunctionName("echo")
public static String echo(
@HttpTrigger(name = "req", methods = { HttpMethod.PUT }, authLevel = AuthorizationLevel.ANONYMOUS, route = "items/{id}") String inputReq,
@TableInput(name = "item", tableName = "items", partitionKey = "Example", rowKey = "{id}", connection = "AzureWebJobsStorage") TestInputData inputData,
@TableOutput(name = "myOutputTable", tableName = "Person", connection = "AzureWebJobsStorage") OutputBinding<Person> testOutputData
) {
testOutputData.setValue(new Person(httpbody + "Partition", httpbody + "Row", httpbody + "Name"));
return "Hello, " + inputReq + " and " + inputData.getKey() + ".";
}
public static class TestInputData {
public String getKey() { return this.rowKey; }
private String rowKey;
}
public static class Person {
public String partitionKey;
public String rowKey;
public String name;
public Person(String p, String r, String n) {
this.partitionKey = p;
this.rowKey = r;
this.name = n;
}
}
}
```


You invoke this function with an HTTP request.

- HTTP request payload is passed as a
`String`

for the argument`inputReq`

. - One entry is retrieved from Table storage, and is passed as
`TestInputData`

to the argument`inputData`

.

To receive a batch of inputs, you can bind to `String[]`

, `POJO[]`

, `List<String>`

, or `List<POJO>`

.

```
@FunctionName("ProcessIotMessages")
public void processIotMessages(
@EventHubTrigger(name = "message", eventHubName = "%AzureWebJobsEventHubPath%", connection = "AzureWebJobsEventHubSender", cardinality = Cardinality.MANY) List<TestEventData> messages,
final ExecutionContext context)
{
context.getLogger().info("Java Event Hub trigger received messages. Batch size: " + messages.size());
}
public class TestEventData {
public String id;
}
```


This function gets triggered whenever there's new data in the configured event hub. Because the `cardinality`

is set to `MANY`

, the function receives a batch of messages from the event hub. `EventData`

from event hub gets converted to `TestEventData`

for the function execution.

### Output binding example

You can bind an output binding to the return value by using `$return`

.

```
package com.example;
import com.microsoft.azure.functions.annotation.*;
public class Function {
@FunctionName("copy")
@StorageAccount("AzureWebJobsStorage")
@BlobOutput(name = "$return", path = "samples-output-java/{name}")
public static String copy(@BlobTrigger(name = "blob", path = "samples-input-java/{name}") String content) {
return content;
}
}
```


If there are multiple output bindings, use the return value for only one of them.

To send multiple output values, use `OutputBinding<T>`

defined in the `azure-functions-java-library`

package.

```
@FunctionName("QueueOutputPOJOList")
public HttpResponseMessage QueueOutputPOJOList(@HttpTrigger(name = "req", methods = { HttpMethod.GET,
HttpMethod.POST }, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "itemsOut", queueName = "test-output-java-pojo", connection = "AzureWebJobsStorage") OutputBinding<List<TestData>> itemsOut,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String query = request.getQueryParameters().get("queueMessageId");
String queueMessageId = request.getBody().orElse(query);
itemsOut.setValue(new ArrayList<TestData>());
if (queueMessageId != null) {
TestData testData1 = new TestData();
testData1.id = "msg1"+queueMessageId;
TestData testData2 = new TestData();
testData2.id = "msg2"+queueMessageId;
itemsOut.getValue().add(testData1);
itemsOut.getValue().add(testData2);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + queueMessageId).build();
} else {
return request.createResponseBuilder(HttpStatus.INTERNAL_SERVER_ERROR)
.body("Did not find expected items in CosmosDB input list").build();
}
}
public static class TestData {
public String id;
}
```


You invoke this function on an `HttpRequest`

object. It writes multiple values to Queue storage.

## HttpRequestMessage and HttpResponseMessage

These helper types, which are designed to work with HTTP Trigger functions, are defined in `azure-functions-java-library`

:

| Specialized type | Target | Typical usage |
|---|---|---|
`HttpRequestMessage<T>` |
HTTP Trigger | Gets method, headers, or queries |
`HttpResponseMessage` |
HTTP Output Binding | Returns status other than 200 |

## Metadata

Few triggers send [trigger metadata](functions-triggers-bindings) along with input data. You can use annotation `@BindingName`

to bind to trigger metadata.

```
package com.example;
import java.util.Optional;
import com.microsoft.azure.functions.annotation.*;
public class Function {
@FunctionName("metadata")
public static String metadata(
@HttpTrigger(name = "req", methods = { HttpMethod.GET, HttpMethod.POST }, authLevel = AuthorizationLevel.ANONYMOUS) Optional<String> body,
@BindingName("name") String queryValue
) {
return body.orElse(queryValue);
}
}
```


In the preceding example, the `queryValue`

is bound to the query string parameter `name`

in the HTTP request URL, `http://{example.host}/api/metadata?name=test`

. Here's another example, showing how to bind to `Id`

from queue trigger metadata.

```
@FunctionName("QueueTriggerMetadata")
public void QueueTriggerMetadata(
@QueueTrigger(name = "message", queueName = "test-input-java-metadata", connection = "AzureWebJobsStorage") String message,@BindingName("Id") String metadataId,
@QueueOutput(name = "output", queueName = "test-output-java-metadata", connection = "AzureWebJobsStorage") OutputBinding<TestData> output,
final ExecutionContext context
) {
context.getLogger().info("Java Queue trigger function processed a message: " + message + " with metadataId:" + metadataId );
TestData testData = new TestData();
testData.id = metadataId;
output.setValue(testData);
}
```


Note

The name provided in the annotation needs to match the metadata property.

## Execution context

`ExecutionContext`

, defined in the `azure-functions-java-library`

, contains helper methods that are used to communicate with the functions runtime. For more information, see the [ExecutionContext reference article](/en-us/java/api/com.microsoft.azure.functions.executioncontext).

### Logger

Use `getLogger`

, defined in `ExecutionContext`

, to write logs from function code.

Example:

```
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
public class Function {
public String echo(@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) String req, ExecutionContext context) {
if (req.isEmpty()) {
context.getLogger().warning("Empty request body received by function " + context.getFunctionName() + " with invocation " + context.getInvocationId());
}
return String.format(req);
}
}
```


## View logs and trace

You can use the Azure CLI to stream Java stdout and stderr logging, and other application logging.

Here's how to configure your function app to write application logging by using the Azure CLI:

```
az webapp log config --name functionname --resource-group myResourceGroup --application-logging true
```


To stream logging output for your function app by using the Azure CLI, open a new command prompt, Bash, or Terminal session, and enter the following command:

The [az webapp log tail](/en-us/cli/azure/webapp/log) command has options to filter output by using the `--provider`

option.

To download the log files as a single ZIP file by using the Azure CLI, open a new command prompt, Bash, or Terminal session, and enter the following command:

```
az webapp log download --resource-group resourcegroupname --name functionappname
```


You must enable file system logging in the Azure portal or the Azure CLI before running this command.

## Environment variables

In Functions, [app settings](functions-app-settings), such as service connection strings, are exposed as environment variables during execution. You can access these settings by using, `System.getenv("AzureWebJobsStorage")`

.

The following example gets the [application setting](functions-how-to-use-azure-function-app-settings#settings), with the key named `myAppSetting`

:

```
public class Function {
public String echo(@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) String req, ExecutionContext context) {
context.getLogger().info("My app setting value: "+ System.getenv("myAppSetting"));
return String.format(req);
}
}
```


## Use dependency injection in Java Functions

Azure Functions Java supports the dependency injection (DI) software design pattern, which is a technique to achieve [Inversion of Control (IoC)](/en-us/dotnet/architecture/modern-web-apps-azure/architectural-principles#dependency-inversion) between classes and their dependencies. Java Azure Functions provides a hook to integrate with popular Dependency Injection frameworks in your Functions Apps. [Azure Functions Java SPI](https://github.com/Azure/azure-functions-java-additions/tree/dev/azure-functions-java-spi) contains an interface [FunctionInstanceInjector](https://github.com/Azure/azure-functions-java-additions/blob/dev/azure-functions-java-spi/src/main/java/com/microsoft/azure/functions/spi/inject/FunctionInstanceInjector.java). By implementing this interface, you can return an instance of your function class and your functions are invoked on this instance. This gives frameworks like [Spring](/en-us/azure/developer/java/spring-framework/getting-started-with-spring-cloud-function-in-azure?toc=%2Fazure%2Fazure-functions%2Ftoc.json), [Quarkus](/en-us/azure/azure-functions/functions-create-first-quarkus), Google Guice, Dagger, etc. the ability to create the function instance and register it into their IOC container. This means you can use those Dependency Injection frameworks to manage your functions naturally.

Note

Microsoft Azure Functions Java SPI Types ([azure-function-java-spi](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-spi/1.0.0)) is a package that contains all SPI interfaces for third parties to interact with Microsoft Azure functions runtime.

### Function instance injector for dependency injection

[azure-function-java-spi](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-spi/1.0.0) contains an interface FunctionInstanceInjector

```
package com.microsoft.azure.functions.spi.inject;
/**
* The instance factory used by DI framework to initialize function instance.
*
* @since 1.0.0
*/
public interface FunctionInstanceInjector {
/**
* This method is used by DI framework to initialize the function instance. This method takes in the customer class and returns
* an instance create by the DI framework, later customer functions will be invoked on this instance.
* @param functionClass the class that contains customer functions
* @param <T> customer functions class type
* @return the instance that will be invoked on by azure functions java worker
* @throws Exception any exception that is thrown by the DI framework during instance creation
*/
<T> T getInstance(Class<T> functionClass) throws Exception;
}
```


For more examples that use FunctionInstanceInjector to integrate with Dependency injection frameworks refer to [this](https://github.com/Azure/azure-functions-java-worker/tree/dev/samples/dependency-injection-example) repository.

## Next steps

For more information about Azure Functions Java development, see the following resources:

[Best practices for Azure Functions](functions-best-practices)[Azure Functions developer reference](functions-reference)[Azure Functions triggers and bindings](functions-triggers-bindings)- Local development and debug with
[Visual Studio Code](https://code.visualstudio.com/docs/java/java-azurefunctions),[IntelliJ](functions-create-maven-intellij), and[Eclipse](functions-create-maven-eclipse) [Remote Debug Java functions using Visual Studio Code](https://code.visualstudio.com/docs/java/java-serverless#_remote-debug-functions-running-in-the-cloud)[Maven plugin for Azure Functions](https://github.com/Microsoft/azure-maven-plugins/blob/develop/azure-functions-maven-plugin/README.md)- Streamline function creation through the
`azure-functions:add`

goal, and prepare a staging directory for[ZIP file deployment](deployment-zip-push).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migration/migrate-aws-lambda-to-azure-functions -->

# Migrate AWS Lambda workloads to Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Migrating a serverless workload that uses Amazon Web Services (AWS) Lambda to Azure Functions requires careful planning and implementation. This article provides essential guidance to help you:

- Perform a discovery process on your existing workload.
- Learn how to perform key migration activities like premigration planning and workload assessment.
- Evaluate and optimize a migrated workload.

## Scope

This article describes the migration of an AWS Lambda instance to Azure Functions.

This article doesn't address:

- Migration to your own container hosting solution, such as through Azure Container Apps.
- Hosting AWS Lambda containers in Azure.
- Fundamental Azure adoption approaches by your organization, such as
[Azure landing zones](/en-us/azure/cloud-adoption-framework/ready/landing-zone/)or other topics addressed in the Cloud Adoption Framework[migrate methodology](/en-us/azure/cloud-adoption-framework/migrate/).

## Migration custom chat mode

To make it easier to migrate your AWS Lambda apps to Azure using Visual Studio Code, Azure Functions provides a [custom chat mode](https://code.visualstudio.com/docs/copilot/customization/custom-chat-modes) in GitHub Copilot. Use these steps to add the `LambdaToFunctionMigration`

custom chat mode to your project in Visual Studio Code:

If you don't already have the

[GitHub Copilot for Azure](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azure-github-copilot)Visual Studio Code extension, install it now.Open your Lambda project as a workspace in Visual Studio Code.

Run this prompt in

**Agent**mode in GitHub Copilot:`Help me migrate my Lambda app to Azure`

When prompted in the notification area, select

**Install**to add the`LambdaToFunctionMigration`

custom chat mode to your project.

You can now use guided prompts defined in this custom chat for each stage of your migration. Start typing `/LambdaMigration`

in chat to see the complete list of available commands.

### Compare functionality

This article maps AWS Lambda features to Azure Functions equivalents to help ensure compatibility.

Important

You might choose to include optimization in your migration plan, but Microsoft recommends a two-step process. Migrate "like-to-like" functionalities first, and then evaluate optimization opportunities on Azure.

Optimization efforts should be continuous and run through your workload team's change control processes. A migration that adds more capabilities during a migration incurs risk and unnecessarily extends the process.

### Workload perspective

This article focuses on how to migrate an AWS Lambda workload to Azure Functions and the common dependencies for serverless workloads. This process might involve several services because workloads comprise many resources and processes to manage those resources. To have a comprehensive strategy, you must combine the recommendations presented in this article with a larger plan that includes the other components and processes in your workload.

## Perform a discovery process on your existing workload

The first step is to conduct a detailed discovery process to evaluate your existing AWS Lambda workload. The goal is to understand which AWS features and services your workload relies on. Compile a comprehensive inventory of your AWS Lambda functions by using AWS tooling like service-specific SDKs, APIs, CloudTrail, and AWS CLI to assess the workload on AWS. You should understand the following key aspects of your AWS Lambda inventory:

- Use cases
- Configurations
- Security and networking setups
- Tooling, monitoring, logging, and observability mechanisms
- Dependencies
- Reliability objectives and current reliability status
- Cost of ownership
- Performance targets and current performance

Tip

Use this custom chat mode prompt to generate an assessment report for your AWS Lambda setup:

```
/LambdaMigration-Phase1-AssessLambdaProject
```


## Perform premigration planning

Before you start migrating your workload, you must map AWS Lambda features to Azure Functions to ensure compatibility and develop a migration plan. Then you can select key workloads for a proof of concept.

You also need to [map the AWS services](/en-us/azure/architecture/aws-professional) that Lambda depends on to the equivalent dependencies in Azure.

## Map AWS Lambda features to Azure Functions

The following tables compare AWS Lambda concepts, resources, and properties with their corresponding equivalents on Azure Functions, specifically, the Flex Consumption hosting plan.

[Supported languages](#supported-languages)[Programming model](#programming-model)[Event triggers and bindings](#event-triggers-and-bindings)[Permissions](#permissions)[Function URL](#function-url)[Networking](#networking)[Observability and monitoring](#observability-and-monitoring)[Scaling and concurrency](#scaling-and-concurrency)[Cold-start protection](#cold-start-protection)[Pricing](#pricing)[Source code storage](#source-code-storage)[Local development](#local-development)[Deployment](#deployment)[Time-out and memory limits](#time-out-and-memory-limits)[Secret management](#secret-management)[State management](#state-management)[Stateful orchestration](#stateful-orchestration)[Other differences and considerations](#other-differences-and-considerations)

### Supported languages

| Programming language |
|
|---|

[Azure Functions supported versions](/en-us/azure/azure-functions/supported-languages)

[Custom handlers](/en-us/azure/azure-functions/functions-custom-handlers)[OS-only runtime](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-provided.html)[Custom handlers](/en-us/azure/azure-functions/functions-custom-handlers)[OS-only runtime](https://docs.aws.amazon.com/lambda/latest/dg/runtimes-provided.html)[Custom handlers](/en-us/azure/azure-functions/functions-custom-handlers)### Programming model

| Feature | AWS Lambda | Azure Functions |
|---|---|---|
| Triggers | Integrates with other AWS services via event sources. Provides automatic and programmatic ways to link Lambda functions with event sources. | Triggers a function based on specific events, such as updates in a database or a new message in a queue. For example, an Azure Cosmos DB trigger allows functions to automatically respond to inserts and updates in an Azure Cosmos DB container. This action enables real-time processing of data changes. Functions also integrates with Azure Event Grid, so it can process events from Azure services, like Azure Storage and Azure Media Services, and external event sources. Event Grid serves as a centralized, extensible event routing service that complements Functions triggers and enables high scalability and broad event-source coverage. |
| Bindings | Doesn't have bindings. Uses AWS SDKs within Lambda functions to manually manage interactions with other AWS services. | Bindings, configured as input or output, enable declarative connections to services, which minimize the need for explicit SDK code. For example, you can configure bindings to read from Blob Storage, write to Azure Cosmos DB, or send emails via SendGrid without manually managing the integrations. |

### Event triggers and bindings

| AWS Lambda trigger or service |
|
|---|

[HTTP trigger](/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger)[Azure Queue Storage trigger](/en-us/azure/azure-functions/functions-bindings-storage-queue-trigger)or[Azure Service Bus trigger](/en-us/azure/azure-functions/functions-bindings-service-bus-trigger)[Event Grid trigger](/en-us/azure/azure-functions/functions-bindings-event-grid-trigger)or[Service Bus trigger](/en-us/azure/azure-functions/functions-bindings-service-bus-trigger)[Event Hubs trigger](/en-us/azure/azure-functions/functions-bindings-event-hubs-trigger)[Azure Cosmos DB change feed trigger](/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-trigger)[Timer trigger](/en-us/azure/azure-functions/functions-bindings-timer)[Blob Storage trigger](/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger)[Azure SQL trigger](/en-us/azure/azure-functions/functions-bindings-azure-sql-trigger)[Apache Kafka trigger](/en-us/azure/azure-functions/functions-bindings-kafka-trigger)[Azure Redis trigger](/en-us/azure/azure-functions/functions-bindings-cache)[RabbitMQ trigger](/en-us/azure/azure-functions/functions-bindings-rabbitmq-trigger)### Permissions

| AWS Lambda | Azure Functions |
|---|---|
| The Lambda execution role grants Lambda functions permissions to interact with other AWS services. Each Lambda function has an associated identity and access management (IAM) role that determines its permissions while it runs. | Managed identities provide an identity for your function app that allows it to authenticate with other Azure services without storing credentials in the code. Role-based access control assigns appropriate roles to the managed identity in Microsoft Entra ID to grant access to the resources that it requires. |
| Resource-based policy statements: - AWSLambda_FullAccess gives full access to all Lambda operations, including creating, updating, and deleting functions. - AWSLambda_ReadOnlyAccess gives read-only access to view Lambda functions and their configurations. - Custom IAM policies. |
Resource-based built-in roles: - The Owner role gives full access, including access permissions management. - The Contributor role can create and delete function apps, configure settings, and deploy code. It can't manage access. - The Monitoring Reader role can grant read-only access to monitoring data and settings. It can also allocate custom roles. |

### Function URL

| AWS Lambda | Azure Functions |
|---|---|
`https://<url-id>.lambda-url.<region>.on.aws` |
- `<appname>.azurewebsites.net` (original, global default hostname) - `<appname>-<randomhash>.<Region>.azurewebsites.net` (new, unique default hostname) |

### Networking

| AWS Lambda | Azure Functions |
|---|---|
| All Lambda functions run securely inside a default system-managed virtual private cloud (VPC). You can also configure your Lambda function to access resources in a custom VPC. | Function apps can be network secured and can access other services inside the network. Inbound network access can be restricted to only a firewall list of IP addresses and to a specific virtual network via service endpoints or private endpoints. Outbound network access is enabled through the virtual network integration feature. The function app can have all its traffic restricted to a virtual network's subnet and can also access other services inside that virtual network. |

### Observability and monitoring

| AWS Lambda | Azure Functions |
|---|---|
| Amazon CloudWatch helps with monitoring and observability by collecting and tracking metrics, aggregating and analyzing logs, setting alarms, creating custom dashboards, and implementing automated responses to changes in resource performance and metrics. | Azure Monitor provides comprehensive monitoring and observability for Azure Functions, particularly through its Application Insights feature. Application Insights collects telemetry data such as request rates, response times, and failure rates. It visualizes application component relationships, monitors real-time performance, logs detailed diagnostics, and allows custom metric tracking. These capabilities help maintain the performance, availability, and reliability of Azure Functions, while enabling custom dashboards, alerts, and automated responses. |
| AWS Lambda generates telemetry data from your function invocations and can export this data by using OpenTelemetry semantics. You can configure your Lambda functions to send this telemetry data to any OpenTelemetry-compliant endpoint. This action allows for correlation of traces and logs, consistent standards-based telemetry data, and integration with other observability tools that support OpenTelemetry. | Configure your functions app to export log and trace data in an OpenTelemetry format. You can export telemetry data to any compliant endpoint by using OpenTelemetry. OpenTelemetry provides benefits such as correlation of traces and logs, consistent standards-based telemetry data, and integration with other providers. You can enable OpenTelemetry at the function app level in the host configuration and in your code project to optimize data exportation from your function code. For more information, see
|

### Scaling and concurrency

| AWS Lambda | Azure Functions |
|---|---|
| AWS uses an on-demand scaling model. Automatically scale your function operation in response to demand. Concurrency, or the number of requests handled by an instance, is always 1. | Instances are dynamically added and removed based on the number of incoming events and the configured concurrency for each instance. You can configure the
|

### Cold-start protection

| AWS Lambda | Azure Functions |
|---|---|
| Provisioned concurrency reduces latency and ensures predictable function performance by pre-initializing a requested number of function instances. Provisioned concurrency suits latency-sensitive applications and is priced separately from standard concurrency. | Function apps allow you to configure concurrency for each instance, which drives its scale. Multiple jobs can run in parallel in the same instance of the app, and subsequent jobs in the instance don't incur the initial cold start. Function apps also have always ready instances. Customers can specify a number of prewarmed instances to eliminate cold-start latency and ensure consistent performance. Function apps also scale out to more instances based on demand, while maintaining the always ready instances. |
| Reserved concurrency specifies the maximum number of concurrent instances that a function can have. This limit ensures that a portion of your account's concurrency quota is set aside exclusively for that function. AWS Lambda dynamically scales out to handle incoming requests even when reserved concurrency is set, as long as the requests don't exceed the specified reserved concurrency limit. The lower limit for reserved concurrency in AWS Lambda is 1. The upper limit for reserved concurrency in AWS Lambda is determined by the account's regional concurrency quota. By default, this limit is 1,000 concurrent operations for each region. | Azure Functions doesn't have an equivalent feature to reserved concurrency. To achieve similar functionality, isolate specific functions into separate function apps and set the maximum scale-out limit for each app. Azure Functions dynamically scales out, or adds more instances, and scales in, or removes instances, within the scale-out limit set. By default, apps that run in a Flex Consumption plan start with a configurable limit of 100 overall instances. The lowest maximum instance count value is 40, and the highest supported maximum instance count value is 1,000.
|

### Pricing

| AWS Lambda | Azure Functions |
|---|---|
| - Pay per use for the total invocation count and for the GB/s for each instance (with a fixed concurrency of 1) - 1 ms increments - 400,000 Gbps free tier |
- Pay per use for the total invocation count and for the GB/s of each instance (with configurable concurrent invocations) - 100 ms increments - 100,000 Gbps free tier -
|

### Source code storage

| AWS Lambda | Azure Functions |
|---|---|
| AWS Lambda manages the storage of your function code in its own managed storage system. You don't need to supply more storage. | Functions requires a customer-supplied Blob Storage container to maintain the deployment package that contains your app's code. You can configure the settings to use the same or a different storage account for deployments and manage authentication methods for accessing the container. |

### Local development

| AWS Lambda feature | Azure Functions feature |
|---|---|
| - SAM CLI -
|
- Azure Functions Core Tools - Visual Studio Code - Visual Studio - GitHub Codespaces - VSCode.dev - Maven -
|

### Deployment

| Feature | AWS Lambda | Azure Functions |
|---|---|---|
| Deployment package | - ZIP file - Container image |
ZIP file (For container image deployment, use the dedicated or premium SKU.) |
| ZIP file size (console) | 50 MB maximum | 500 MB maximum for ZIP deployment |
| ZIP file size (CLI/SDK) | 250 MB maximum for ZIP deployment, 500 MB maximum for unzipped | 500 MB maximum for ZIP deployment |
| Container image size | 10 GB maximum | Container support with flexible storage via Azure |
| Large artifact handling | Use container images for larger deployments. | Attach Blob Storage or Azure Files shares to access large files from the app. |
| Packaging common dependencies to functions | Layers | Deployment .Zip, on demand from storage, or containers (ACA, dedicated, EP SKUs only) |
| Blue-green deployment or function versioning | Use function qualifiers to reference a specific state of your function by using either a version number or an alias name. Qualifiers enable version management and gradual deployment strategies. | Use continuous integration and continuous delivery systems for blue-green deployments. |

### Time-out and memory limits

| Feature | AWS Lambda limits | Azure Functions limits |
|---|---|---|
| Execution time-out | 900 seconds (15 minutes) | The default time-out is 30 minutes. The maximum time-out is unbounded. However, the grace period given to a function execution is 60 minutes during scale-in and 10 minutes during platform updates. For more information, see
|

[2-GB and 4-GB](/en-us/azure/azure-functions/functions-scale#service-limits)instance sizes. Each region in a given subscription has a memory limit of 512,000 MB for all instances of apps, which you can increase by calling support. The total memory usage of all instances across all function apps in a region must stay within this quota.Although 2 GB and 4 GB are the instance size options, the concurrency for each instance can be higher than 1. Therefore, a single instance can handle multiple concurrent executions, depending on the configuration. Configuring concurrency appropriately can help optimize resource usage and manage performance. By balancing memory allocation and concurrency settings, you can effectively manage the resources allocated to your function apps and ensure efficient performance and cost control. For more information, see

[Regional subscription memory quotas](/en-us/azure/azure-functions/flex-consumption-plan#regional-subscription-memory-quotas).### Secret management

| AWS Lambda | Azure Functions |
|---|---|
| AWS Secrets Manager allows you to store, manage, and retrieve secrets such as database credentials, API keys, and other sensitive information. Lambda functions can retrieve secrets by using the AWS SDK. | We recommend that you use secretless approaches like managed identities to enable secure access to Azure resources without hardcoding credentials. When secrets are required, such as for partner or legacy systems, Azure Key Vault provides a secure solution to store and manage secrets, keys, and certificates. |
| AWS Systems Manager Parameter Store is a service that stores configuration data and secrets. Parameters can be encrypted by using AWS KMS and retrieved by Lambda functions by using the AWS SDK. Lambda functions can store configuration settings in environment variables. Sensitive data can be encrypted with a KMS key for secure access. |
Azure Functions uses application settings to store configuration data. These settings map directly to environment variables for ease of use within the function. These settings can be encrypted and securely stored in the Azure App Service configuration. For more advanced scenarios, Azure App Configuration provides robust features for managing multiple configurations. It enables feature flagging and supports dynamic updates across services. |

### State management

| AWS Lambda | Azure Functions |
|---|---|
| AWS Lambda handles simple state management by using services like Amazon S3 for object storage, DynamoDB for fast and scalable NoSQL state storage, and SQS for message queue handling. These services ensure data persistence and consistency across Lambda function executions. | Azure Functions uses `AzureWebJobsStorage` to manage state by enabling bindings and triggers with Azure Storage services like Blob Storage, Queue Storage, and Table Storage. It allows functions to easily read and write state. For more complex state management, Durable Functions provides advanced workflow orchestration and state persistence capabilities by using Azure Storage. |

### Stateful orchestration

| AWS Lambda | Azure Functions |
|---|---|
| No native state orchestration. Use AWS Step Functions for workflows. | Durable Functions helps with complex state management by providing durable workflow orchestration and stateful entities. It enables long-running operations, automatic checkpointing, and reliable state persistence. These features enable building intricate workflows to ensure fault tolerance and scalability for stateful applications. |

### Other differences and considerations

| Feature | AWS Lambda | Azure Functions |
|---|---|---|
| Grouping functions | Each AWS Lambda function is an independent entity. | A function app serves as a container for multiple functions. It provides a shared execution context and configuration for the functions that it contains. Treating multiple functions as a single entity simplifies deployment and management. Functions also uses a per-function scaling strategy, where each function is scaled independently, except for HTTP, Blob Storage, and Durable Functions triggers. These triggered functions scale in their own groups. |
| Custom domains | Enabled via API Gateway | You can
|

[custom containers that run in an Container Apps environment](/en-us/azure/azure-functions/functions-how-to-custom-container).## Create a migration plan

Select key workloads for a proof of concept.

Start by selecting one to two medium-sized, noncritical workloads from your total inventory. These workloads serve as the foundation for your proof-of-concept migration. You can test the process and identify potential challenges without risking major disruption to your operations.

Test iteratively and gather feedback.

Tip

Use this custom chat mode prompt to check the current status of the migration process at any time:

`/LambdaMigration-GetStatus`

Use the proof of concept to gather feedback, identify gaps, and fine-tune the process before you scale to larger workloads. This iterative approach ensures that by the time you move to full-scale migration, you address potential challenges and refine the process.


## Build the migration assets

This step is a transitional development phase. During this phase, you build source code, infrastructure as code (IaC) templates, and deployment pipelines to represent the workload in Azure. You must adapt function code for compatibility and best practices before you can perform the migration.

[Adapt function code, configuration files, and infrastructure as code files](#adapt-function-code-configuration-files-and-infrastructure-as-code-files)Tip

Use this custom chat mode prompt to start the code migration process:

`/LambdaMigration-Phase2-MigrateLambdaCode`

[Adjust configuration settings](#adjust-configuration-settings)[Generate IaC files](#generate-iac-files)[Use tools for refactoring](#use-tools-for-refactoring)

### Adapt function code, configuration files, and infrastructure as code files

To update code for Azure Functions runtime requirements:

Modify your code to adhere to the Azure Functions programming model. For instance, adapt your function signatures to match the format that Azure Functions requires. For more information about function definition and execution context, see

[Azure Functions developer guides](/en-us/azure/azure-functions/functions-reference-node).Use the

[Azure Functions extensions bundle](/en-us/azure/azure-functions/functions-bindings-register)to handle various bindings and triggers that are similar to AWS services. For .NET applications, you should use the appropriate NuGet packages instead of the extensions bundle.Use the extensions bundle to integrate with other Azure services such as Azure Storage, Azure Service Bus, and Azure Cosmos DB without needing to manually configure each binding through SDKs. For more information, see

[Connect functions to Azure services by using bindings](/en-us/azure/azure-functions/add-bindings-existing-function)and[Azure Functions binding expression patterns](/en-us/azure/azure-functions/functions-bindings-expressions-patterns).

These snippets are examples of common SDK code. The AWS Lambda code maps to the corresponding triggers, bindings, or SDK code snippets in Azure Functions.

**Reading from Amazon S3 versus Azure Blob Storage**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const s3 = new AWS.S3();
exports.handler = async (event) => {
const params = {
Bucket: 'my-bucket',
Key: 'my-object.txt',
};
const data = await
s3.getObject(params).promise();
console.log('File content:',
data.Body.toString());
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.storageblob('blobTrigger', {
path: 'my-container/{blobName}',
connection: 'AzureWebJobsStorage',
}, async (context, myBlob) => {
context.log(`Blob content:
${myBlob.toString()}`);
});
```


**Writing to Amazon Simple Queue Service (SQS) versus Azure Queue Storage**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const sqs = new AWS.SQS();
exports.handler = async (event) => {
const params = {
QueueUrl:
'https://sqs.amazonaws.com/123456789012/MyQueue',
MessageBody: 'Hello, world!',
};
await
sqs.sendMessage(params).promise();
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.queue('queueTrigger', {
queueName: 'myqueue-items',
connection: 'AzureWebJobsStorage',
}, async (context, queueMessage) => {
context.log(`Queue message:
${queueMessage}`);
});
```


**Writing to DynamoDB versus Azure Cosmos DB**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const dynamoDb = new AWS.DynamoDB.DocumentClient();
exports.handler = async (event) => {
const params = {
TableName: 'my-table',
Key: { id: '123' },
};
const data = await dynamoDb.get(params).promise();
console.log('DynamoDB record:', data.Item);
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.cosmosDB('cosmosTrigger', {
connectionStringSetting: 'CosmosDBConnection',
databaseName: 'my-database',
containerName: 'my-container',
leaseContainerName: 'leases',
}, async (context, documents) => {
documents.forEach(doc => {
context.log(`Cosmos DB document: ${JSON.stringify(doc)}`);
});
});
```


**Amazon CloudWatch Events versus an Azure timer trigger**

AWS Lambda code (SDK)

```
exports.handler = async (event) => {
console.log('Scheduled event:', event);
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.timer('timerTrigger', { schedule: '0 */5 * * * *', // Runs every 5 minutes }, async (context, myTimer) => { if (myTimer.isPastDue) { context.log('Timer is running late!'); } context.log(Timer function executed at: ${new Date().toISOString()}); });
```


**Amazon Simple Notification Service (SNS) versus an Azure Event Grid trigger**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const sns = new AWS.SNS();
exports.handler = async (event) => {
const params = {
Message: 'Hello, Event Grid!',
TopicArn: 'arn:aws:sns:us-east-1:123456789012:MyTopic',
};
await sns.publish(params).promise();
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.eventGrid('eventGridTrigger', {},
async (context, eventGridEvent) => {
context.log(`Event Grid event:
${JSON.stringify(eventGridEvent)}`);
});
```


**Amazon Kinesis versus an Azure Event Hubs trigger**

AWS Lambda code (SDK)

```
const AWS = require('aws-sdk');
const kinesis = new AWS.Kinesis();
exports.handler = async (event) => {
const records =
event.Records.map(record =>
Buffer.from(record.kinesis.data,
'base64').toString());
console.log('Kinesis records:', records);
};
```


Azure Functions code (trigger)

```
import { app } from '@azure/functions';
app.eventHub('eventHubTrigger', {
connection: 'EventHubConnection',
eventHubName: 'my-event-hub',
}, async (context, eventHubMessages) =>
{
eventHubMessages.forEach(message =>
{
context.log(`Event Hub message:
${message}`);
});
});
```


See the following GitHub repositories to compare AWS Lambda code and Azure Functions code:

[AWS Lambda code](https://github.com/MadhuraBharadwaj-MSFT/TestLambda)[Azure Functions code](https://github.com/MadhuraBharadwaj-MSFT/TestAzureFunction)[Azure samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples), which includes starter, IaC, and end-to-end samples for Azure Functions

### Adjust configuration settings

Ensure that your function's time-out and [memory](/en-us/azure/azure-functions/flex-consumption-how-to#configure-instance-memory) settings are compatible with Azure Functions. For more information about configurable settings, see [host.json reference for Azure Functions](/en-us/azure/azure-functions/functions-host-json).

Follow the recommended best practices for permissions, access, networking, and deployment configurations.

#### Configure permissions

Follow best practices when you set up permissions on your function apps. For more information, see [Configure your function app and storage account with managed identity](https://eng.ms/docs/cloud-ai-platform/devdiv/serverless-paas-balam/serverless-paas-vikr/app-service-web-apps/app-service-team-documents/functionteamdocs/faqs/tutorial-secretless-mi#configure-your-function-app-and-storage-account-with-managed-identity).

**main.bicep**

```
// User-assigned managed identity that the function app uses to reach Storage and Service Bus
module processorUserAssignedIdentity './core/identity/userAssignedIdentity.bicep' = {
name: 'processorUserAssignedIdentity'
scope: rg
params: {
location: location
tags: tags
identityName: !empty(processorUserAssignedIdentityName) ? processorUserAssignedIdentityName : '${abbrs.managedIdentityUserAssignedIdentities}processor-${resourceToken}'
}
}
```


For more information, see [rbac.bicep](https://github.com/Azure-Samples/functions-quickstart-javascript-azd/blob/main/infra/app/rbac.bicep).

#### Configure network access

Azure Functions supports [virtual network integration](/en-us/azure/azure-functions/functions-networking-options#virtual-network-integration), which gives your function app access to resources in your virtual network. After integration, your app routes outbound traffic through the virtual network. Then your app can access private endpoints or resources by using rules that only allow traffic from specific subnets. If the destination is an IP address outside of the virtual network, the source IP address is one of the addresses listed in your app's properties, unless you configure a NAT gateway.

When you enable [virtual network integration](/en-us/azure/azure-functions/flex-consumption-how-to#enable-virtual-network-integration) for your function apps,
follow the best practices in [TSG for virtual network integration for web apps and function apps](https://eng.ms/docs/cloud-ai-platform/devdiv/serverless-paas-balam/serverless-paas-vikr/app-service-web-apps/app-service-team-documents/functionteamdocs/faqs/tsg-vnet-integration).

**main.bicep**

```
// Virtual network and private endpoint
module serviceVirtualNetwork 'app/vnet.bicep' = {
name: 'serviceVirtualNetwork'
scope: rg
params: {
location: location
tags: tags
vNetName: !empty(vNetName) ? vNetName : '${abbrs.networkVirtualNetworks}${resourceToken}'
}
}
module servicePrivateEndpoint 'app/storage-PrivateEndpoint.bicep' = {
name: 'servicePrivateEndpoint'
scope: rg
params: {
location: location
tags: tags
virtualNetworkName: !empty(vNetName) ? vNetName : '${abbrs.networkVirtualNetworks}${resourceToken}'
subnetName: serviceVirtualNetwork.outputs.peSubnetName
resourceName: storage.outputs.name
}
}
```


For more information, see [VNet.bicep](https://github.com/Azure-Samples/functions-quickstart-javascript-azd/blob/main/infra/app/vnet.bicep) and [storage-PrivateEndpoint.bicep](https://github.com/Azure-Samples/functions-quickstart-javascript-azd/blob/main/infra/app/storage-PrivateEndpoint.bicep).

#### Configure deployment settings

Deployments follow a single path. After you build your project code and zip it into an application package, deploy it to a Blob Storage container. When it starts, your app gets the package and runs your function code from it. By default, the same storage account that stores internal host metadata, such as `AzureWebJobsStorage`

, also serves as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by configuring your app's deployment settings. For more information, see [Deployment technology details](/en-us/azure/azure-functions/functions-deployment-technologies#deployment-technology-details) and [Configure deployment settings](/en-us/azure/azure-functions/flex-consumption-how-to#configure-deployment-settings).

### Generate IaC files

Use tools like Bicep, Azure Resource Manager templates, or Terraform to create IaC files to deploy Azure resources.

Tip

Use this custom chat mode prompt to generate infrastructure as code (IaC) files for Azure Functions:

`/LambdaMigration-Phase3-GenerateFunctionsInfra`

Define resources such as Azure Functions, storage accounts, and networking components in your IaC files.

Use this

[IaC samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC)for samples that use Azure Functions recommendations and best practices.

### Use tools for refactoring

Use tools like GitHub Copilot in VS Code for help with code refactoring, manual refactoring for specific changes, or other migration aids.

Note

Use *Agent mode* in GitHub Copilot in VS Code.

The following articles provide specific examples and detailed steps to facilitate the migration process:

## Develop a step-by-step process for Day-0 migration

Develop failover and failback strategies for your migration and thoroughly test them in a preproduction environment. We recommend that you perform end-to-end testing before you finally transition from AWS Lambda to Azure Functions.

Validate functionality

Test each function thoroughly to ensure that it works as expected. These tests should include input/output, event triggers, and bindings verification.

Tip

Use this custom chat mode prompt to validate the migrated Azure Functions code:

`/LambdaMigration-Phase4-ValidateCode`

Use tools like curl or

[REST Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)extensions on VS Code to send HTTP requests for HTTP-triggered functions.For other triggers, such as timers or queues, ensure that the triggers fire correctly and the functions run as expected.


Validate performance

Conduct performance testing to compare the new Azure Functions deployment with the previous AWS Lambda deployment.

Monitor metrics like response time, run time, and resource consumption.

Tip

Use this custom chat mode prompt to validate the infrastructure configuration:

`/LambdaMigration-Phase5-ValidateInfra`

Use Application Insights for

[monitoring, log analysis, and troubleshooting](/en-us/azure/azure-functions/functions-monitoring)during the testing phase.

Troubleshoot by using the diagnose and solve problems feature

Use the

[diagnose and solve problems](/en-us/azure/app-service/overview-diagnostics)feature in the Azure portal to troubleshoot your function app. This tool provides a set of diagnostics features that can help you quickly identify and resolve common problems, such as application crashes, performance degradation, and configuration problems. Follow the guided troubleshooting steps and recommendations that the tool provides to address problems that you identify.

## Evaluate the end state of the migrated workload

Before you decommission resources in AWS, you need to be confident that the platform meets current workload expectations and that nothing blocks workload maintenance or further development.

Deploy and test functions to validate their performance and correctness.

### Deploy to Azure

Tip

Use this custom chat mode prompt to deploy the validated project to Azure:

```
/LambdaMigration-Phase6-DeployToAzure
```


Deploy workloads by using the [VS Code](/en-us/azure/azure-functions/functions-develop-vs-code#publish-to-azure) publish feature. You can also deploy workloads from the command line by using [Azure Functions Core Tools](/en-us/azure/azure-functions/functions-run-local#project-file-deployment) or the [Azure CLI](/en-us/cli/azure/functionapp/deployment/source#az-functionapp-deployment-source-config-zip). [Azure DevOps](/en-us/azure/azure-functions/functions-how-to-azure-devops#deploy-your-app) and [GitHub Actions](/en-us/azure/azure-functions/functions-how-to-github-actions) also use One Deploy.

Azure Functions Core Tools:

[Deploy your function app](/en-us/azure/azure-functions/flex-consumption-how-to#deploy-your-code-project)by using[Azure Functions Core Tools](/en-us/azure/azure-functions/functions-run-local)with the`func azure functionapp publish <FunctionAppName>`

command.Continuous integration and continuous deployment (CI/CD) pipelines: Set up a CI/CD pipeline by using services like GitHub Actions, Azure DevOps, or another CI/CD tool.


For more information, see [Continuous delivery by using GitHub Actions](/en-us/azure/azure-functions/functions-how-to-github-actions) or [Continuous delivery with Azure Pipelines](/en-us/azure/azure-functions/functions-how-to-azure-devops).

## Explore sample migration scenarios

Use the [MigrationGetStarted repo](https://github.com/MadhuraBharadwaj-MSFT/MigrationGetStarted) as a template to begin your proof of concept. This repo includes a ready-to-deploy Azure Functions project that has the infrastructure and source code files to help you get started.

If you prefer to use Terraform, use [MigrationGetStarted-Terraform](https://github.com/MadhuraBharadwaj-MSFT/MigrationGetStarted-Terraform) instead.

## Optimize and monitor the application's performance on Azure

After you migrate your workload, we recommend that you explore more features on Azure. These features might help you fulfill future workload requirements and help close gaps.

### Use Application Insights for monitoring and troubleshooting

Enable [Application Insights](/en-us/azure/azure-functions/functions-monitoring) for your function app to collect detailed telemetry data for monitoring and troubleshooting. You can enable Application Insights through the Azure portal or in the function app's host.json configuration file. After you enable Application Insights, you can:

Collect telemetry data. Application Insights provides various telemetry data such as request logs, performance metrics, exceptions, and dependencies.

Analyze logs and metrics. Access the Application Insights dashboard from the Azure portal to visualize and analyze logs, metrics, and other telemetry data. Use the built-in tools to create custom queries and visualize data to gain insights into the performance and behavior of your function app.

Set up alerts. Configure alerts in Application Insights to notify you of critical problems, performance degradation, or specific events. These alerts help you proactively monitor and quickly respond to problems.


### Optimize for cost and performance

Scaling and performance optimization:

Use autoscaling features to handle varying workloads efficiently.

Optimize function code to improve performance by reducing run time, optimizing dependencies, and using efficient coding practices.

Implement caching strategies to reduce repeated processing and latency for frequently accessed data.


Cost management:

Use

[Microsoft Cost Management](/en-us/azure/cost-management-billing/cost-management-billing-overview)tools to monitor and analyze your Azure Functions costs.Set up budgeting and cost alerts to manage and predict expenses effectively.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/migration/migrate-plan-consumption-to-flex -->

# Migrate Consumption plan apps to the Flex Consumption plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides step-by-step instructions for migrating your existing function apps hosted in the [Consumption plan](../consumption-plan) in Azure Functions to instead use the [Flex Consumption plan](../flex-consumption-plan).

The way you migrate your app to the Flex Consumption plan depends on whether your app runs on Linux or on Windows. Make sure to select your operating system at the top of the article.

Tip

Azure Functions provides Azure CLI commands in [ az functionapp flex-migration](/en-us/cli/azure/functionapp/flex-migration) that automate most of the steps required to move your Linux app from the Consumption to the Flex Consumption plan. This article features these commands, which are currently only supported for apps running on Linux.

When you migrate your existing serverless apps, your functions can take advantage of these benefits of the Flex Consumption plan:

**Enhanced performance**: your apps benefit from improved scalability and always-ready instances to reduce cold start impacts.**Improved controls**: fine-tune your functions with per-function scaling and concurrency settings.**Expanded networking**: virtual network integration and private endpoints let you run your functions in both public and private networks.**Future platform investment**: as the top serverless hosting plan, current and future investments are made on Flex Consumption first for platform stability, performance, and features.

The Flex Consumption plan is the recommended serverless hosting option for your functions going forward. For more information, see [Flex Consumption plan benefits](../flex-consumption-plan#benefits). For a detailed comparison between hosting plans, see [Azure Functions hosting options](../functions-scale).

## Considerations

Before starting a migration, keep these considerations in mind:

If you're running Consumption plan function apps on Azure Government regions, review this guidance now to prepare for migration until Flex Consumption is enabled in Azure Government.

Due to the significant configuration and behavior differences between the two plans, you aren't able to

*shift*an existing Consumption plan app to the Flex Consumption plan. The migration process instead has you create a new Flex Consumption plan app that's equivalent to your current app. This new app runs in the same resource group and with the same dependencies as your current app.You should prioritize the migration of your apps that run in a Consumption plan on Linux.

This article assumes that you have a general understanding of Functions concepts and architectures and are familiar with features of your apps being migrated. Such concepts include triggers and bindings, authentication, and networking customization.

This article shows you how to both evaluate the current app and deploy your new Flex Consumption plan app using either the

[Azure portal](https://portal.azure.com)or the[Azure CLI](/en-us/cli/azure). If your current app deployment is defined by using infrastructure-as-code (IaC), you can generally follow the same steps. You can perform the same actions directly in your ARM templates or Bicep files, with these resource-specific considerations:- The Flex Consumption plan introduced a new section in the
`Microsoft.Web/sites`

resource type called`functionAppConfig`

, which contains many of the configurations that were application settings. For more information, see[Flex Consumption plan deprecations](../functions-app-settings#flex-consumption-plan-deprecations). - You can find resource configuration details for a Flex Consumption plan app in
[Automate resource deployment for your function app in Azure Functions](../functions-infrastructure-as-code?pivots=flex-consumption-plan). - Functions maintains a set of canonical Flex Consumption plan deployment examples for
[ARM templates](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/armtemplate),[Bicep files](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/bicep), and[Terraform files](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC).

- The Flex Consumption plan introduced a new section in the

## Prerequisites

Access to the Azure subscription containing one or more function apps to migrate. The account used to run Azure CLI commands must be able to:

- Create and manage function apps and App Service hosting plans.
- Assign roles to managed identities.
- Create and manage storage accounts.
- Create and manage Application Insights resources.
- Access all dependent resources of your app, such as Azure Key Vault, Azure Service Bus, or Azure Event Hubs.

Being assigned to the

**Owner**or**Contributor**roles in your resource group generally provides sufficient permissions.[Azure CLI](/en-us/cli/azure), version v2.77.0, or a later version. Scripts are tested using Azure CLI in[Azure Cloud Shell](/en-us/azure/cloud-shell/overview).The

[resource-graph](../../governance/resource-graph/first-query-azurecli)extension, which you can install by using thecommand:`az extension add`

`az extension add --name resource-graph`

The

, which is used to work with JSON output.`jq`

tool

## Identify potential apps to migrate

Use these steps to make a list of the function apps you need to migrate. In this list, make note of their names, resource groups, locations, and runtime stacks. You can then repeat the steps in this guide for each app you decide to migrate to the Flex Consumption plan.

The way that function app information is maintained depends on whether your app runs on Linux or Windows.

For Linux Consumption apps, use the new [ az functionapp flex-migration list](/en-us/cli/azure/functionapp/flex-migration#az-functionapp-flex-migration-list) command to identify apps that are eligible for migration:

```
az functionapp flex-migration list
```


This command automatically scans your subscription and returns two arrays:

**eligible_apps**: Linux Consumption apps that can be migrated to Flex Consumption. These apps are compatible with Flex Consumption.**ineligible_apps**: Apps that can't be migrated, along with the specific reasons why. The reasons for incompatibility need to be reviewed and addressed before continuing.

Note

This command only evaluates function apps running on the **Linux Consumption plan**. Apps running on other hosting plans (Windows Consumption, Premium, Dedicated, or Flex Consumption) won't appear in either the `eligible_apps`

or `ineligible_apps`

arrays. If you have many function apps and aren't sure which hosting plan each one uses, you can run `az functionapp list --query "[].{name:name, sku:sku}" -o table`

to see all apps and their SKUs, where `Dynamic`

indicates a Consumption plan app.

The output includes the app name, resource group, location, and runtime stack for each app, along with eligibility status and migration readiness information.

Use this [ az graph query](/en-us/cli/azure/graph#az-graph-query) command to list all function apps in your subscription that are running in a Consumption plan:

```
az graph query -q "resources | where subscriptionId == '$(az account show --query id -o tsv)' \
| where type == 'microsoft.web/sites' | where ['kind'] == 'functionapp' | where properties.sku == 'Dynamic' \
| project name, location, resourceGroup" \
--query data --output table
```


This command generates a table with the app name, location, and resource group for all Consumption apps running on Windows in the current subscription.

You're prompted to install the [resource-graph extension](/en-us/cli/azure/graph), if it isn't already installed.

## Assess your existing app

Before migrating to the Flex Consumption plan, you should perform these checks to make sure that your function app can be migrated successfully:

### Confirm region compatibility

Confirm that the Flex Consumption plan is currently supported in the same region as the Consumption plan app you intend to migrate.


Confirmed:When the`az functionapp flex-migration list`

command output has your app in the`eligible_apps`

list, the Flex Consumption plan is supported in the same region used by your current Linux Consumption app. In this case, you can continue to[Verify language stack compatibility].


Action required:When the`az functionapp flex-migration list`

command output has your app in the`ineligible_apps`

list, you see an error message stating`The site '<name>' is not in a region supported in Flex Consumption. Please see the list regions supported in Flex Consumption by running az functionapp list-flexconsumption-locations`

. In this case, the Flex Consumption plan isn't yet supported in the region used by your current Linux Consumption app.

Use this [ az functionapp list-flexconsumption-locations](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-locations) command to list all regions where Flex Consumption plan is available:

```
az functionapp list-flexconsumption-locations --query "sort_by(@, &name)[].{Region:name}" -o table
```


This command generates a table of Azure regions where the Flex Consumption plan is currently supported.

If your region isn't currently supported and you still choose to migrate your function app, your app must run in a different region where the Flex Consumption plan is supported. However, running your app in a different region from other connected services can introduce extra latency. Make sure that the new region can meet your application's performance requirements before you complete the migration.

### Verify language stack compatibility

Flex Consumption plans don't yet support all [Functions language stacks](../supported-languages). This table indicates which language stacks are currently supported:

| Stack setting | Stack name | Supported |
|---|---|---|
`dotnet-isolated` |
|

`node`

[JavaScript/TypeScript](../functions-reference-node)`java`

[Java](../functions-reference-java)`python`

`powershell`

[PowerShell](../functions-reference-powershell)`dotnet`

[.NET (in-process model)](../functions-dotnet-class-library)`custom`

[Custom handlers](../functions-custom-handlers)

Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already using a supported language stack by Flex Consumption and you can continue to[Verify stack version compatibility].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`Runtime '<name>' not supported for function apps on the Flex Consumption plan.`

, your Linux Consumption app isn't running a supported runtime by Flex Consumption yet.

If your function app uses an unsupported runtime stack:

- For C# apps that run in-process with the runtime (
`dotnet`

), you must first migrate your app to .NET isolated. For more information, see[Migrate C# apps from the in-process model to the isolated worker model](../migrate-dotnet-to-isolated-model).

### Verify stack version compatibility

Before migrating, you must make sure that your app's runtime stack version is supported when running in a Flex Consumption plan in the current region.


Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already using a supported language stack version by Flex Consumption and you can continue to[Verify deployment slots usage].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`Invalid version {0} for runtime {1} for function apps on the Flex Consumption plan. Supported versions for runtime {1} are {2}.`

, your Linux Consumption app isn't running a supported runtime by Flex Consumption yet.

Use this [ az functionapp list-flexconsumption-runtimes](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-runtimes) command to verify Flex Consumption plan support for your language stack version in a specific region:

```
az functionapp list-flexconsumption-runtimes --location <REGION> --runtime <LANGUAGE_STACK> --query '[].{version:version}' -o tsv
```


In this example, replace `<REGION>`

with your current region and `<LANGUAGE_STACK>`

with one of these values:

| Language stack | Value |
|---|---|
|

`dotnet-isolated`

[Java](../functions-reference-java)`java`

[JavaScript](../functions-reference-node)`node`

[PowerShell](../functions-reference-powershell)`powershell`

[Python](../functions-reference-python)`python`

[TypeScript](../functions-reference-node)`node`

This command displays all versions of the specified language stack supported by the Flex Consumption plan in your region.

If your function app uses an unsupported language stack version, you must first [upgrade your app code to a supported version](../update-language-versions) before migrating to the Flex Consumption plan.

### Verify deployment slots usage

Consumption plan apps can have a deployment slot defined. For more information, see [Azure Functions deployment slots](../functions-deployment-slots). However, the Flex Consumption plan doesn't currently support deployment slots. Before you migrate, you must determine if your app has a deployment slot. If so, you need to define a strategy for how to manage your app without deployment slots when running in a Flex Consumption plan.


Confirmed:When your current app has deployment slots enabled, the`az functionapp flex-migration list`

command shows your function app in the`eligible_apps`

list without a warning, continue to[Verify the use of certificates].


Action required:Your current app has deployment slots enabled, the`az functionapp flex-migration list`

command shows your function app in the`eligible_apps`

list but adds a warning that states:`The site '<name>' has slots configured. This will not block migration, but please note that slots are not supported in Flex Consumption.`


Use this [ az functionapp deployment slot list](/en-us/cli/azure/functionapp/deployment/slot#az-functionapp-deployment-slot-list) command to list any deployment slots defined in your function app:

```
az functionapp deployment slot list --name <APP_NAME> --resource-group <RESOURCE_GROUP> --output table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. If the command returns an entry, your app has deployment slots enabled.

If your function app is currently using deployment slots, you can't currently reproduce this functionality in the Flex Consumption plan. Before migrating, you should:

- Consider rearchitecting your application to use separate function apps. In this way, you can develop, test, and deploy your function code to a second nonproduction app instead of using slots, or
- Migrate any new code or features from the deployment slot into the main (
**production**) slot.

### Verify the use of certificates

Transport Layer Security (TLS) certificates, previously known as Secure Sockets Layer (SSL) certificates, are used to help secure internet connections. TSL/SSL certificates, which include managed certificates, bring-your-own certificates (BYOC), or public-key certificates, aren't currently supported by the Flex Consumption plan.


Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already not using certificates, and you can continue to[Verify your Blob storage triggers].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`The site '<name>' is using TSL/SSL certificates. TSL/SSL certificates are not supported in Flex Consumption.`

or`The site '<name>' has the WEBSITE_LOAD_CERTIFICATES app setting configured. Certificate loading is not supported in Flex Consumption.`

, your Linux Consumption app isn't yet compatible with Flex Consumption.

Use the [ az webapp config ssl list](/en-us/cli/azure/webapp/config/ssl#az-webapp-config-ssl-list) command to list any TSL/SSL certificates available to your function app:

```
az webapp config ssl list --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

with your resource group name. If this command produces output, your app is likely using certificates.

If your app currently relies on TSL/SSL certificates, you shouldn't proceed with the migration until after support for certificates is added to the Flex Consumption plan.

### Verify your Blob storage triggers

Currently, the Flex Consumption plan only supports event-based triggers for Azure Blob storage, which are defined with a `Source`

setting of `EventGrid`

. Blob storage triggers that use container polling and use a `Source`

setting of `LogsAndContainerScan`

aren't supported in Flex Consumption. Because container polling is the default, you must determine if any of your Blob storage triggers are using the default `LogsAndContainerScan`

source setting. For more information, see [Trigger on a blob container](../storage-considerations#trigger-on-a-blob-container).


Confirmed:If the`az functionapp flex-migration list`

command included your app in the`eligible_apps`

list, your Linux Consumption app is already not using a blob storage triggers with`EventGrid`

as the source. You can continue to[Consider dependent services].


Action required:If the`az functionapp flex-migration list`

command included your app in the`ineligible_apps`

list with an error message stating`The site '<name>' has blob storage trigger(s) that don't use Event Grid as the source: <list> Flex Consumption only supports Event Grid-based blob triggers. Please convert these triggers to use Event Grid or replace them with Event Grid triggers before migration.`

, your Linux Consumption app isn't yet compatible with Flex Consumption.

Use this [`az functionapp function list`

] command to determine if your app has any Blob storage triggers that don't use Event Grid as the source:

```
az functionapp function list --name <APP_NAME> --resource-group <RESOURCE_GROUP> \
--query "[?config.bindings[0].type=='blobTrigger' && config.bindings[0].source!='EventGrid'].{Function:name,TriggerType:config.bindings[0].type,Source:config.bindings[0].source}" \
--output table
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. If the command returns rows, there is at least one trigger using container polling in your function app.

If your app has any Blob storage triggers that don't have an Event Grid source, you must change to an Event Grid source before you migrate to the Flex Consumption plan.

The basic steps to change an existing Blob storage trigger to an Event Grid source are:

Add or update the

`source`

property in your Blob storage trigger definition to`EventGrid`

and redeploy the app.[Build the endpoint URL](../functions-event-grid-blob-trigger#build-the-endpoint-url)in your function app used to be used by the event subscription.[Create an event subscription](../functions-event-grid-blob-trigger#create-the-event-subscription)on your Blob storage container.

For more information, see [Tutorial: Trigger Azure Functions on blob containers using an event subscription](../functions-event-grid-blob-trigger).

## Consider dependent services

Because Azure Functions is a compute service, you must consider the effect of migration on data and services both upstream and downstream of your app.

### Data protection strategies

Here are some strategies to protect both upstream and downstream data during the migration:

**Idempotency**: Ensure your functions can safely process the same message multiple times without negative side effects. For more information, see[Designing Azure Functions for identical input](../functions-idempotent).**Logging and monitoring**: Enable detailed logging in both apps during migration to track message processing. For more information, see[Monitor executions in Azure Functions](../functions-monitoring).**Checkpointing**: For streaming triggers, such as the Event Hubs trigger, implement correct checkpoint behaviors to track processing position. For more information, see[Azure Functions reliable event processing](../functions-reliable-event-processing).**Parallel processing**: Consider temporarily running both apps in parallel during the cutover. Make sure to carefully monitor and validate how data is processed from the upstream service. For more information, see[Active-active pattern for non-HTTPS trigger functions](/en-us/azure/reliability/reliability-functions#active-active-pattern-for-non-https-trigger-functions).**Gradual cutover**: For high-volume systems, consider implementing a gradual cutover by redirecting portions of traffic to the new app. You can manage the routing of requests upstream from your apps by using services such as[Azure API Management](../functions-openapi-definition)or[Azure Application Gateway](../../app-service/overview-app-gateway-integration).

### Mitigations by trigger type

You should plan mitigation strategies to protect data for the specific function triggers you might have in your app:

| Trigger | Risk to data | Strategy |
|---|---|---|
|

With the new app running, switch clients to use the new container.

Allow the original container to be processed completely before stopping the old app.

[Azure Cosmos DB](../functions-bindings-cosmosdb-v2-trigger)Set this new lease container as the

`leaseCollectionName`

configuration in your new app.Requires that your

[functions be idempotent](../functions-idempotent)or you must be able to handle the results of duplicate change feed processing.Set the

`StartFromBeginning`

configuration to `false`

in the new app to avoid reprocessing the entire feed.[Azure Event Grid](../functions-bindings-event-grid-trigger)Requires that your

[functions be idempotent](../functions-idempotent)or you must be able to handle the results of duplicate event processing.[Azure Event Hubs](../functions-bindings-event-hubs-trigger)[consumer group](../../event-hubs/event-hubs-features#consumer-groups)for use by the new app. For more information, see[Migration strategies for Event Grid triggers](../functions-reliable-event-processing#migration-strategies-for-event-grid-triggers).[Azure Service Bus](../functions-bindings-service-bus-trigger)Update senders and clients to use the new topic or queue.

After the original topic is empty, shut down the old app.

[Azure Storage queue](../functions-bindings-storage-queue-trigger)Update senders and clients to use the new queue.

After the original queue is empty, shut down the old app.

[HTTP](../functions-bindings-http-webhook-trigger)[Timer](../functions-bindings-timer)[Disable the timer trigger](../disable-function)in the old app after the new app runs successfully.## Start the migration for Linux

The [az functionapp flex-migration start](/en-us/cli/azure/functionapp/flex-migration#az-functionapp-flex-migration-start) command automatically collects application configuration information and creates a new Flex Consumption app with the same configurations as the source app. Use the command as shown in this example:

```
az functionapp flex-migration start \
--source-name <SOURCE_APP_NAME> \
--source-resource-group <SOURCE_RESOURCE_GROUP> \
--name <NEW_APP_NAME> \
--resource-group <RESOURCE_GROUP>
```


In this example, replace these placeholders with the indicated values:

| Placeholder | Value |
|---|---|
`<SOURCE_APP_NAME>` |
The name of your original app. |
`<SOURCE_RESOURCE_GROUP>` |
The resource group of the original app. |
`<NEW_APP_NAME>` |
The name of the new app. |
`<RESOURCE_GROUP>` |
The resource group of the new app. |

The `az functionapp flex-migration start`

command performs these basic tasks:

- Assesses your source app for compatibility with the Flex Consumption hosting plan.
- Creates a function app in the Flex Consumption plan.
- Migrates most configurations including app settings, identity assignments, storage mounts, CORS settings, custom domains, and access restrictions.

### Command Options

The migration command supports several options to customize the migration:

| Option | Description |
|---|---|
`--storage-account` |
Specify a different storage account for the new app |
`--maximum-instance-count` |
Set the maximum number of instances for scaling |
`--skip-access-restrictions` |
Skip migrating IP access restrictions |
`--skip-cors` |
Skip migrating CORS settings |
`--skip-hostnames` |
Skip migrating custom domains |
`--skip-managed-identities` |
Skip migrating managed identity configurations |
`--skip-storage-mount` |
Skip migrating storage mount configurations |

For complete command options, use `az functionapp flex-migration start --help`

.

After you've completed running `az functionapp flex-migration start`

successfully, continue to [Get the code deployment package](#get-the-code-deployment-package).

## Premigration tasks

Before proceeding with the migration, you must collect key information about and resources used by your Consumption plan app to help make a smooth transition to running in the Flex Consumption plan.

You should complete these tasks before you migrate your app to run in a Flex Consumption plan:

### Collect app settings

If you plan to use the same trigger and bindings sources and other settings from app settings, you need to first take note of the current app settings in your existing Consumption plan app.

Use this [ az functionapp config appsettings list](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-list) command to return an

`app_settings`

object that that contains the existing app setting as JSON:```
app_settings=$(az functionapp config appsettings list --name `<APP_NAME>` --resource-group `<RESOURCE_GROUP>`)
echo $app_settings
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively.

Caution

App settings frequently contain keys and other shared secrets. Always store applications settings securely, ideally encrypted. For improved security, you should use Microsoft Entra ID authentication with managed identities in the new Flex Consumption plan app instead of shared secrets.

### Collect application configurations

There are other app configurations not found in app settings. You should also capture these configurations from your existing app so that you can be sure to properly recreate them in the new app.

Review these settings. If any of them exist in the current app, you must decide whether they must also be recreated in the new Flex Consumption plan app:

| Configuration | Setting | Comment |
|---|---|---|
| CORS settings | `cors` |
Determines any existing cross-origin resource sharing (CORS) settings, which your clients might require. |
| Custom domains | If your app is currently using a domain other than `*.azurewebsites.net` , you would need to replace this custom domain mapping with a mapping to your new app. |
|
| HTTP version | `http20Enabled` |
Determines if HTTP 2.0 is required by your app. |
| HTTPS only | `httpsOnly` |
Determines if TSL/SSL is required to access your app. |
| Incoming client certificates | `clientCertEnabled` `clientCertMode` `clientCertExclusionPaths` |
Sets requirements for client requests that use certificates for authentication. |
| Maximum scale-out limit | `WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT` |
Sets the limit on scaled-out instances. The default maximum value is 200. This value is found in your app settings, but in a Flex Consumption plan app it instead gets added as a site setting (`maximumInstanceCount` ). |
| Minimum inbound TLS version | `minTlsVersion` |
Sets a minimum version of TLS required by your app. |
| Minimum inbound TLS Cipher | `minTlsCipherSuite` |
Sets a minimum TLS cipher requirement for your app. |
| Mounted Azure Files shares | `azureStorageAccounts` |
Determines if any explicitly mounted file shares exist in your app (Linux-only). |
| SCM basic auth publishing credentials | `scm.allow` |
Determines if the
`scm` publishing site is enabled |

[publishing methods](../functions-deployment-technologies)require it.

Use this script to obtain the relevant application configurations of your existing app:

```
# Set the app and resource group names
appName=<APP_NAME>
rgName=<RESOURCE_GROUP>
echo "Getting commonly used site settings..."
az functionapp config show --name $appName --resource-group $rgName \
--query "{http20Enabled:http20Enabled, httpsOnly:httpsOnly, minTlsVersion:minTlsVersion, \
minTlsCipherSuite:minTlsCipherSuite, clientCertEnabled:clientCertEnabled, \
clientCertMode:clientCertMode, clientCertExclusionPaths:clientCertExclusionPaths}"
echo "Checking for SCM basic publishing credentials policies..."
az resource show --resource-group $rgName --name scm --namespace Microsoft.Web \
--resource-type basicPublishingCredentialsPolicies --parent sites/$appName --query properties
echo "Checking for the maximum scale-out limit configuration..."
az functionapp config appsettings list --name $appName --resource-group $rgName \
--query "[?name=='WEBSITE_MAX_DYNAMIC_APPLICATION_SCALE_OUT'].value" -o tsv
echo "Checking for any file share mount configurations..."
az webapp config storage-account list --name $appName --resource-group $rgName
echo "Checking for any custom domains..."
az functionapp config hostname list --webapp-name $appName --resource-group $rgName --query "[?contains(name, 'azurewebsites.net')==\`false\`]" --output table
echo "Checking for any CORS settings..."
az functionapp cors show --name $appName --resource-group $rgName
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. If any of the site settings or checks return non-null values, make a note of them.

### Identify managed identities and role-based access

Before migrating, you should document whether your app relies on the system-assigned managed identity or any user-assigned managed identities. You must also determine the role-based access control (RBAC) permissions granted to these identities. You must recreate the system-assigned managed identity and any role assignments in your new app. You should be able to reuse your user-assigned managed identities in your new app.

This script checks for both the system-assigned managed identity and any user-assigned managed identities associated with your app:

```
appName=<APP_NAME>
rgName=<RESOURCE_GROUP>
echo "Checking for a system-assigned managed identity..."
systemUserId=$(az functionapp identity show --name $appName --resource-group $rgName --query "principalId" -o tsv)
if [[ -n "$systemUserId" ]]; then
echo "System-assigned identity principal ID: $systemUserId"
echo "Checking for role assignments..."
az role assignment list --assignee $systemUserId --all
else
echo "No system-assigned identity found."
fi
echo "Checking for user-assigned managed identities..."
userIdentities=$(az functionapp identity show --name $appName --resource-group $rgName --query 'userAssignedIdentities' -o json)
if [[ "$userIdentities" != "{}" && "$userIdentities" != "null" ]]; then
echo "$userIdentities" | jq -c 'to_entries[]' | while read -r identity; do
echo "User-assigned identity name: $(echo "$identity" | jq -r '.key' | sed 's|.*/userAssignedIdentities/||')"
echo "Checking for role assignments..."
az role assignment list --assignee $(echo "$identity" | jq -r '.value.principalId') --all --output json
echo
done
else
echo "No user-assigned identities found."
fi
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. Make a note of all identities and their role assignments.

### Identify built-in authentication settings

Before migrating to Flex Consumption, you should collect information about any built-in authentication configurations. If you want to have your app use the same client authentication behaviors, you must recreate them in the new app. For more information, see [Authentication and authorization in Azure Functions](../../app-service/overview-authentication-authorization).

Pay special attention to redirect URIs, allowed external redirects, and token settings to ensure a smooth transition for authenticated users.

Use this [ az webapp auth show](/en-us/cli/azure/webapp/auth#az-webapp-auth-show) command to determine if

[built-in authentication](../../app-service/overview-authentication-authorization)is configured in your function app:

```
az webapp auth show --name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively. Review the output to determine if authentication is enabled and which identity providers are configured.

You should recreate these setting in your new app post-migration so that your clients can maintain access using their preferred provider.

### Review inbound access restrictions

It's possible to set [inbound access restrictions](../functions-networking-options#inbound-access-restrictions) on apps in a Consumption plan. You might want to maintain these restrictions in your new app. For each restriction defined, make sure to capture these properties:

- IP addresses or CIDR ranges
- Priority values
- Action type (Allow/Deny)
- Names of the rules

This [ az functionapp config access-restriction show] command returns a list of any existing IP-based access restrictions:

```
az functionapp config access-restriction show --name <APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group name and app name, respectively.

When running in the Flex Consumption plan, you can recreate these inbound IP-based restrictions. You can further secure your app by implementing other networking restrictions, such as virtual network integration and inbound private endpoints. For more information, see [Virtual network integration](../flex-consumption-plan#virtual-network-integration).

## Get the code deployment package

To be able to redeploy your app, you must have either your project's source files or the deployment package. Ideally, your project files are maintained in source control so that you can easily redeploy function code to your new app. If you have your source code files, you can skip this section and continue to [Capture performance benchmarks (optional)](#capture-performance-benchmarks-optional).

If you no longer have access to your project source files, you can download the current deployment package from the existing Consumption plan app in Azure. The location of the deployment package depends on whether you run on Linux or Windows.

Consumption plan apps on Linux maintain the deployment zip package file in one of these locations:

An Azure Blob storage container named

`scm-releases`

in the default host storage account (`AzureWebJobsStorage`

). This container is the default deployment source for a Consumption plan app on Linux.If your app has a

`WEBSITE_RUN_FROM_PACKAGE`

setting that is a URL, the package is in an externally accessible location that you maintain. An external package should be hosted in a blob storage container with restricted access. For more information, see[External package URL](../functions-deployment-technologies#external-package-url).

Tip

If your storage account is restricted to managed identity access only, you might need to grant your Azure account read access to the storage container by adding it to the `Storage Blob Data Reader`

role.

The deployment package is compressed using the `squashfs`

format. To see what's inside the package, you must use tools that can decompress this format.

Use these steps to download the deployment package from your current app:

Use this

command to get the`az functionapp config appsettings list`

`WEBSITE_RUN_FROM_PACKAGE`

app setting, if present:`az functionapp config appsettings list --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --query "[?name=='WEBSITE_RUN_FROM_PACKAGE'].value" -o tsv`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name, respectively. If this command returns a URL, then you can download the deployment package file from that remote location and skip to the next section.If the

`WEBSITE_RUN_FROM_PACKAGE`

value is`1`

or nothing, use this script to get the deployment package for the existing app:`appName=<APP_NAME> rgName=<RESOURCE_GROUP> echo "Getting the storage account connection string from app settings..." storageConnection=$(az functionapp config appsettings list --name $appName --resource-group $rgName \ --query "[?name=='AzureWebJobsStorage'].value" -o tsv) echo "Getting the package name..." packageName=$(az storage blob list --connection-string $storageConnection --container-name scm-releases \ --query "[0].name" -o tsv) echo "Download the package? $packageName? (Y to proceed, any other key to exit)" read -r answer if [[ "$answer" == "Y" || "$answer" == "y" ]]; then echo "Proceeding with download..." az storage blob download --connection-string $storageConnection --container-name scm-releases \ --name $packageName --file $packageName else echo "Exiting script." exit 0 fi`

Again, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name. The package .zip file is downloaded to the directory from which you executed the command.

The location of your project source files depends on the `WEBSITE_RUN_FROM_PACKAGE`

app setting as follows:

`WEBSITE_RUN_FROM_PACKAGE` value |
Source file location |
|---|---|
`1` |
The files are in a zip package that is stored in the Azure Files share of the storage account defined by the `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` setting. The name of the files share is defined by the `WEBSITE_CONTENTSHARE` setting. |
| An endpoint URL | The files are in a zip package in an externally accessible location that you maintain. An external package should be hosted in a blob storage container with restricted access. For more information, see
|

Use this

command to get the`az functionapp config appsettings list`

`WEBSITE_RUN_FROM_PACKAGE`

app setting, if present:`az functionapp config appsettings list --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --query "[?name=='WEBSITE_RUN_FROM_PACKAGE'].value" -o tsv`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name, respectively. If this command returns a URL, then you can download the deployment package file from that remote location and skip to the next section.If the

`WEBSITE_RUN_FROM_PACKAGE`

value is`1`

or nothing, use this script to get the deployment package for the existing app:`appName=<APP_NAME> rgName=<RESOURCE_GROUP> echo "Getting the storage account connection string and file share from app settings..." json=$(az functionapp config appsettings list --name $appName --resource-group $rgName \ --query "[?name=='WEBSITE_CONTENTAZUREFILECONNECTIONSTRING' || name=='WEBSITE_CONTENTSHARE'].value" -o json) storageConnection=$(echo "$json" | jq -r '.[0]') fileShare=$(echo "$json" | jq -r '.[1]') echo "Getting the package name..." packageName=$(az storage file list --share-name $fileShare --connection-string $storageConnection \ --path "data/SitePackages" --query "[?ends_with(name, '.zip')] | sort_by(@, &properties.lastModified)[-1].name" \ -o tsv) echo "Download the package? $packageName? (Y to proceed, any other key to exit)" read -r answer if [[ "$answer" == "Y" || "$answer" == "y" ]]; then echo "Proceeding with download..." az storage file download --connection-string $storageConnection --share-name $fileShare \ --path "data/SitePackages/$packageName" else echo "Exiting script." exit 0 fi`

Again, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group name and app name. The package .zip file is downloaded to the directory from which you executed the command.

## Capture performance benchmarks (optional)

If you plan to validate performance improvement in your app based on the migration to the Flex Consumption plan, you should (optionally) capture the performance benchmarks of your current plan. Then, you can compare them to the same benchmarks for your app running in a Flex Consumption plan for comparison.

Tip

Always compare performance under similar conditions, such as time-of-day, day-of-week, and client load. Try to run the two benchmarks as close together as possible.

Here are some benchmarks to consider for your structured performance testing:

| Suggested benchmark | Comment |
|---|---|
Cold-start |
Measure the time from first request to the first response after an idle period. |
Throughput |
Measure the maximum requests-per-second using
|

**Latency**`P50`

, `P95`

, and `P99`

response times under various load conditions. You can monitor these metrics in Application Insights.You can use this Kusto query to review the suggested latency response times in Application Insights:

```
requests
| where timestamp > ago(1d)
| summarize percentiles(duration, 50, 95, 99) by bin(timestamp, 1h)
| render timechart
```


## Migration Steps

The migration of your functions from a Consumption plan app to a Flex Consumption plan app follows these main steps:

### Verify Flex Consumption app created and configured

After running the [az functionapp flex-migration start](/en-us/cli/azure/functionapp/flex-migration#az-functionapp-flex-migration-start) command, you should verify that your new Flex Consumption app was created successfully and properly configured. Here are some steps to validate the migration results:

**Verify the new app exists and is running:**`az functionapp show --name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP> \ --query "{name:name, kind:kind, sku:properties.sku}" --output table`

**Review migrated app settings:**`az functionapp config appsettings list --name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP> \ --output table`

Compare these settings with your source app to ensure critical configurations were transferred.

**Check managed identity configuration:**`az functionapp identity show --name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP>`

**Verify any custom domains were migrated:**`az functionapp config hostname list --webapp-name <NEW_APP_NAME> --resource-group <RESOURCE_GROUP> \ --output table`


### Review Migration Summary

The automated migration command should have transferred most configurations. However, you should manually verify that these items weren't migrated and they might need to be configured manually:

**Certificates**: TSL/SSL certificates aren't supported in Flex Consumption yet**Deployment slots**: Not supported in Flex Consumption**Built-in authentication settings**: These need to be reconfigured manually**CORS settings**: May need manual verification depending on your configuration

If any critical settings are missing or incorrect, you can manually configure them using the steps outlined in the [Windows migration process](#create-an-app-in-the-flex-consumption-plan) sections of this article.

[Final review of the plan](#final-review-of-the-plan)[Create an app in the Flex Consumption plan](#create-an-app-in-the-flex-consumption-plan)[Apply migrated app settings in the new app](#apply-migrated-app-settings-in-the-new-app)[Apply other app configurations](#apply-other-app-configurations)[Configure scale and concurrency settings](#configure-scale-and-concurrency-settings)[Configure any custom domains and CORS access](#configure-any-custom-domains-and-cors-access)[Configure managed identities and assign roles](#configure-managed-identities-and-assign-roles)[Configure Network Access Restrictions](#configure-network-access-restrictions)[Enable monitoring](#enable-monitoring)[Configure built-in authentication](#configure-built-in-authentication)[Deploy Your App Code to the New Flex Consumption App](#deploy-your-app-code-to-the-new-flex-consumption-app)

### Final review of the plan

Before proceeding with the migration process, take a moment to perform these last preparatory steps:

**Review all the collected information**: Go through all the notes, configuration details, and application settings you documented in the previous assessment and premigration sections. If anything is unclear, rerun the Azure CLI commands again or get the information from the portal.**Define your migration plan**: Based on your findings, create a checklist for your migration that highlights:- Any settings that need special attention
- Triggers and bindings or other dependencies that might be affected during migration
- Testing strategy for post-migration validation
- Rollback plan if there are unexpected issues

**Downtime planning**: Consider when to stop the original function app to avoid both data loss and duplicate processing of events, and how this might affect your users or downstream systems. In some cases, you might need to[disable specific functions](../disable-function)before stopping the entire app.

A careful final review helps ensure a smoother migration process and minimizes the risk of overlooking important configurations.

### Create an app in the Flex Consumption plan

There are various ways to create a function app in the Flex Consumption plan along with other required Azure resources:

| Create option | Reference articles |
|---|---|
| Azure CLI |
|

[Create a function app in the Azure portal](../functions-create-function-app-portal)[ARM template](../functions-create-first-function-resource-manager)[azd](../create-first-function-azure-developer-cli)[Bicep](../functions-create-first-function-bicep)[Terraform](../functions-create-first-function-terraform)[Visual Studio Code deployment](../functions-develop-vs-code#publish-to-azure)[Visual Studio deployment](../functions-develop-vs#publish-to-azure)Tip

When possible, you should use Microsoft Entra ID for authentication instead of connection strings, which contain shared keys. Using managed identities is a best practice that improves security by eliminating the need to store shared secrets directly in application settings. If your original app used connection strings, the Flex Consumption plan is designed to support managed identities. Most of these links show you how to enable managed identities in your function app.

### Apply migrated app settings in the new app

Before deploying your code, you must configure the new app with the relevant Flex Consumption plan app settings from your original function app.

Important

Not all Consumption plan app settings are supported when running in a Flex Consumption plan. For more information, see [Flex Consumption plan deprecations](../functions-app-settings#flex-consumption-plan-deprecations).

Run this script that performs these tasks:

- Gets app settings from the old app, ignoring settings that don't apply in a Flex Consumption plan or that already exist in the new app.
- Writes the collected settings locally to a temporary file.
- Applies settings from the file to your new app.
- Deletes the temporary file.

```
sourceAppName=<SOURCE_APP_NAME>
destAppName=<DESTINATION_APP_NAME>
rgName=<RESOURCE_GROUP>
echo "Getting app settings from the old app..."
app_settings=$(az functionapp config appsettings list --name $sourceAppName --resource-group $rgName)
# Filter out settings that don't apply to Flex Consumption apps or that will already have been created
filtered_settings=$(echo "$app_settings" | jq 'map(select(
(.name | ascii_downcase) != "website_use_placeholder_dotnetisolated" and
(.name | ascii_downcase | startswith("azurewebjobsstorage") | not) and
(.name | ascii_downcase) != "website_mount_enabled" and
(.name | ascii_downcase) != "enable_oryx_build" and
(.name | ascii_downcase) != "functions_extension_version" and
(.name | ascii_downcase) != "functions_worker_runtime" and
(.name | ascii_downcase) != "functions_worker_runtime_version" and
(.name | ascii_downcase) != "functions_max_http_concurrency" and
(.name | ascii_downcase) != "functions_worker_process_count" and
(.name | ascii_downcase) != "functions_worker_dynamic_concurrency_enabled" and
(.name | ascii_downcase) != "scm_do_build_during_deployment" and
(.name | ascii_downcase) != "website_contentazurefileconnectionstring" and
(.name | ascii_downcase) != "website_contentovervnet" and
(.name | ascii_downcase) != "website_contentshare" and
(.name | ascii_downcase) != "website_dns_server" and
(.name | ascii_downcase) != "website_max_dynamic_application_scale_out" and
(.name | ascii_downcase) != "website_node_default_version" and
(.name | ascii_downcase) != "website_run_from_package" and
(.name | ascii_downcase) != "website_skip_contentshare_validation" and
(.name | ascii_downcase) != "website_vnet_route_all" and
(.name | ascii_downcase) != "applicationinsights_connection_string"
))')
echo "Settings to migrate..."
echo "$filtered_settings"
echo "Writing settings to a local a local file (app_settings_filtered.json)..."
echo "$filtered_settings" > app_settings_filtered.json
echo "Applying settings to the new app..."
output=$(az functionapp config appsettings set --name $destAppName --resource-group $rgName --settings @app_settings_filtered.json)
echo "Deleting the temporary settings file..."
rm -rf app_settings_filtered.json
echo "Current app settings in the new app..."
az functionapp config appsettings list --name $destAppName --resource-group $rgName
```


In this example, replace `<RESOURCE_GROUP>`

, `<SOURCE_APP_NAME>`

, and `<DEST_APP_NAME>`

with your resource group name and the old a new app names, respectively. This script assumes that both apps are in the same resource group.

### Apply other app configurations

Find the list of other app configurations from your old app that you [collected during premigration](#collect-application-configurations) and also set them in the new app.

In this script, set the value for any configuration set in the original app and comment-out any commands for any configuration not set (`null`

):

```
appName=<APP_NAME>
rgName=<RESOURCE_GROUP>
http20Setting=<YOUR_HTTP_20_SETTING>
minTlsVersion=<YOUR_TLS_VERSION>
minTlsCipher=<YOUR_TLS_CIPHER>
httpsOnly=<YOUR_HTTPS_ONLY_SETTING>
certEnabled=<CLIENT_CERT_ENABLED>
certMode=<YOUR_CLIENT_CERT_MODE>
certExPaths=<CERT_EXCLUSION_PATHS>
scmAllowBasicAuth=<ALLOW_SCM_BASIC_AUTH>
# Apply HTTP version and minimum TLS settings
az functionapp config set --name $appName --resource-group $rgName --http20-enabled $http20Setting
az functionapp config set --name $appName --resource-group $rgName --min-tls-version $minTlsVersion
# Apply the HTTPS-only setting
az functionapp update --name $appName --resource-group $rgName --set HttpsOnly=$httpsOnly
# Apply incoming client cert settings
az functionapp update --name $appName --resource-group $rgName --set clientCertEnabled=$certEnabled
az functionapp update --name $appName --resource-group $rgName --set clientCertMode=$certMode
az functionapp update --name $appName --resource-group $rgName --set clientCertExclusionPaths=$certExPaths
# Apply the TLS cipher suite setting
az functionapp update --name $appName --resource-group $rgName --set minTlsCipherSuite=$minTlsCipher
# Apply the allow scm basic auth configuration
az resource update --resource-group $rgName --name scm --namespace Microsoft.Web --resource-type basicPublishingCredentialsPolicies \
--parent sites/$appName --set properties.allow=$scmAllowBasicAuth
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. Also, replace the placeholders of any variable definitions for existing settings you want to recreate in the new app, and comment-out any `null`

settings.

### Configure scale and concurrency settings

The Flex Consumption plan implements per-function scaling, where each function within your app can scale independently based on its workload. Scaling is also more strictly related to concurrency settings, which are used to make scaling decisions based on the current concurrent executions. For more information, see both [Per-function scaling](../flex-consumption-plan#per-function-scaling) and [Concurrency](../flex-consumption-plan#concurrency) in the Flex Consumption plan article.

Consider concurrency settings first if you want your new app to scale similarly to your original app. Setting higher concurrency values can result in fewer instances being created to handle the same load.

If you had a custom scale-out limit set in your original app, you can also apply it to your new app. Otherwise, you can skip to the next section.

The default maximum instance count is 100, and it must be set to a value of 40 or higher.

Use this [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to set the maximum scale-out.

```
az functionapp scale config set --name <APP_NAME> --resource-group <RESOURCE_GROUP> \
--maximum-instance-count <MAX_SCALE_SETTING>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively. Replace `<MAX_SCALE_SETTING>`

with the maximum scale value you're setting.

### Configure any custom domains and CORS access

If your original app had any bound custom domains or any CORS settings defined, recreate them in your new app. For more information about custom domains, see [Set up an existing custom domain in Azure App Service](../../app-service/app-service-web-tutorial-custom-domain).

Use this

command to rebind any custom domain mappings to your app:`az functionapp config hostname add`

`az functionapp config hostname add --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --hostname <CUSTOM_DOMAIN>`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively. Replace`<CUSTOM_DOMAIN>`

with your custom domain name.Use this

command to replace any CORS settings:`az functionapp cors add`

`az functionapp cors add --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --allowed-origins <ALLOWED_ORIGIN_1> <ALLOWED_ORIGIN_2> <ALLOWED_ORIGIN_N>`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively. Replace`<ALLOWED_ORIGIN_*>`

with your allowed origins.

### Configure managed identities and assign roles

The way that you configure managed identities in your new app depends on the kind of managed identity:

| Managed identity type | Create identity | Role assignments |
|---|---|---|
| User-assigned | Optional | You can continue to use the same user-assigned managed identities with the new app. You must reassign these identities to your Flex Consumption app and verify that they still have the correct role assignments in remote services. If you choose to create new identities for the new app, you must assign the same roles as the existing identities. |
| System-assigned | Yes | Because each function app has its own system-assigned managed identity, you must enable the system-assigned managed identity in the new app and reassign the same roles as in the original app. |

Recreating the role assignments correctly is key to ensuring your function app has the same access to Azure resources after the migration.

Tip

If your original app used connection strings or other shared secrets for authentication, this is a great opportunity to improve your app's security by switching to using Microsoft Entra ID authentication with managed identities. For more information, see [Tutorial: Create a function app that connects to Azure services using identities instead of secrets](../functions-identity-based-connections-tutorial).

Use this

command to enable the system-assigned managed identity in your new app:`az functionapp identity assign`

`az functionapp identity assign --name <APP_NAME> --resource-group <RESOURCE_GROUP>`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively.Use this script to get the principal ID of the system assigned identity and add it to the required roles:

`# Get the principal ID of the system identity principalId=$(az functionapp identity show --name <APP_NAME> --resource-group <RESOURCE_GROUP> \ --query principalId -o tsv) # Assign a role in a specific resource (scope) to the system identity az role assignment create --assignee $principalId --role "<ROLE_NAME>" --scope "<RESOURCE_ID>"`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively. Replace`<ROLE_NAME>`

and`<RESOURCE_ID>`

with the role name and specific resource you captured from the original app.Repeat the previous commands for each role required by the new app.


### Configure Network Access Restrictions

If your original app had any IP-based inbound access restrictions, you can recreate any of the same inbound access rules you want to keep in your new app.

Tip

The Flex Consumption plan [fully supports virtual network integration](../flex-consumption-plan#virtual-network-integration). Because of this, you also have the option to use inbound private endpoints after migration. For more information, see [Private endpoints](../functions-networking-options#private-endpoints).

Use this [ az functionapp config access-restriction add](/en-us/cli/azure/functionapp/config/access-restriction#az-functionapp-config-access-restriction-add) command for each IP access restriction you want to replicate in the new app:

```
az functionapp config access-restriction add --name <APP_NAME> --resource-group <RESOURCE_GROUP> \
--rule-name <RULE_NAME> --action Deny --ip-address <IP_ADDRESS> --priority <PRIORITY>
```


In this example, replace these placeholders with the values from your original app:

| Placeholder | Value |
|---|---|
`<APP_NAME>` |
Your function app name. |
`<RESOURCE_GROUP>` |
Your resource group. |
`<RULE_NAME>` |
Friendly name for the IP rule. |
`<Priority>` |
Priority for the exclusion. |
`<IP_Address>` |
The IP address to exclude. |

Run this command for each documented IP restriction from the original app.

### Enable monitoring

Before you start your new app in the Flex Consumption plan, make sure that Application Insights is enabled. Having Application Insights configured helps you to troubleshoot any issues that might occur during code deployment and start-up.

Implement a comprehensive monitoring strategy that covers app metrics, logs, and costs. By using such a strategy, you can validate the success of your migration, identify any issues promptly, and optimize the performance and cost of your new app.

If you plan to compare this new app with your current app, make sure your scheme also collects the required benchmarks for comparison. For more information, see [Configure monitoring](../flex-consumption-how-to#monitor-your-app-in-azure).

### Configure built-in authentication

If your original app used built-in client authentication (sometimes called Easy Auth), you should recreate it in your new app. If you're planning to reuse the same client registration, make sure to set the new app's authenticated endpoints in the authentication provider.

Based on the information you collected earlier, use the [ az webapp auth update](/en-us/cli/azure/webapp/auth#az-webapp-auth-update) command to recreate each built-in authentication registration required by your app.

### Deploy Your App Code to the New Flex Consumption App

With your new Flex Consumption plan app fully configured based on the settings from the original app, it's time to deploy your code to the new app resources in Azure.

Caution

After successful deployment, triggers in your new app immediately start processing data from connected services. To minimize duplicated data and prevent data loss while starting the new app and shutting-down the original app, you should review the strategies that you defined in [mitigations by trigger type](#mitigations-by-trigger-type).

Functions provides several ways to deploy your code, either from the code project or as a ready-to-run deployment package.

Tip

If your project code is maintained in a source code repository, now is the perfect time to configure a continuous deployment pipeline. Continuous deployment lets you automatically deploy application updates based on changes in a connected repository.

You should update your existing deployment workflows to deploy your source code to your new app:

You can also create a new continuous deployment workflow for your new app. For more information, see [Continuous deployment for Azure Functions](../functions-continuous-deployment)

## Post-migration tasks

After a successful migration, you should perform these follow-up tasks:

### Verify basic functionality

Verify the new app is running in a Flex Consumption plan:

Use this

command two view the details about the hosting plan:`az functionapp show`

`az functionapp show --name <APP_NAME> --resource-group <RESOURCE_GROUP> --query "serverFarmId"`

In this example, replace

`<RESOURCE_GROUP>`

and`<APP_NAME>`

with your resource group and function app names, respectively.Use an HTTP client to call at least one HTTP trigger endpoint on your new app to make sure it responds as expected.


### Capture performance benchmarks

With your new app running, you can run the same performance benchmarks that you collected from your original app, such as:

| Suggested benchmark | Comment |
|---|---|
Cold-start |
Measure the time from first request to the first response after an idle period. |
Throughput |
Measure the maximum requests-per-second using
|

**Latency**`P50`

, `P95`

, and `P99`

response times under various load conditions. You can monitor these metrics in Application Insights.You can use this Kusto query to review the suggested latency response times in Application Insights:

```
requests
| where timestamp > ago(1d)
| summarize percentiles(duration, 50, 95, 99) by bin(timestamp, 1h)
| render timechart
```


Note

Flex Consumption plan metrics differ from Consumption plan metrics. When comparing performance before and after migration, keep in mind that you must use different metrics to track similar performance characteristics. For more information, see [Configure monitoring](../flex-consumption-how-to#monitor-your-app-in-azure).

### Create custom dashboards

Azure Monitor metrics and Application Insights enable you to [create dashboards in the Azure portal](/en-us/azure/azure-portal/azure-portal-dashboards) that display charts from both platform metrics and runtime logs and analytics.

Consider setting-up dashboards and alerts on your key metrics in the Azure portal. For more information, see [Monitor your app in Azure](../flex-consumption-how-to?tabs=azure-portal#monitor-your-app-in-azure).

### Refine plan settings

Actual performance improvements and cost implications of the migration can vary based on your app-specific workloads and configuration. The Flex Consumption plan provides several settings that you can adjust to refine the performance of your app. You might want to make adjustments to more closely match the behavior of the original app or to balance cost versus performance. For more information, see [Fine-tune your app](../flex-consumption-how-to#fine-tune-your-app) in the Flex Consumption article.

### Update your Infrastructure as Code

If you manage your function app infrastructure using Bicep or Terraform, you need to update your IaC files to target the Flex Consumption plan. This section shows the key differences between Consumption and Flex Consumption plan resource definitions.

Important

You can't convert an existing Consumption plan app to Flex Consumption in place. You need to create new resources with a new name or delete the existing resources before deploying the Flex Consumption equivalents.

#### Key differences

When migrating your IaC from Consumption to Flex Consumption, consider these important changes:

| Aspect | Consumption plan | Flex Consumption plan |
|---|---|---|
| Hosting plan SKU | `Y1` (Dynamic) |
`FC1` (FlexConsumption) |
| Plan required | Optional (auto-created) | Required (must be explicit) |
| Operating system | Windows or Linux | Linux only |
| Configuration | App settings | `functionAppConfig` section |
| Storage content share | `WEBSITE_CONTENTSHARE` setting |
`deployment.storage` in `functionAppConfig` |

The examples below demonstrate the key differences between Consumption and Flex Consumption plan resource definitions, and use system assigned managed identity, but they are not complete. They don't include all required resources such as storage accounts, Application Insights, or all necessary role assignments. For complete, production-ready examples, review the [Flex Consumption IaC samples](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC).

**Consumption plan (before):**

```
// Consumption plan (optional - auto-created if omitted)
resource hostingPlan 'Microsoft.Web/serverfarms@2022-03-01' = {
name: hostingPlanName
location: location
sku: {
name: 'Y1'
tier: 'Dynamic'
}
properties: {
reserved: true // Linux
}
}
resource functionApp 'Microsoft.Web/sites@2022-03-01' = {
name: functionAppName
location: location
kind: 'functionapp,linux'
properties: {
serverFarmId: hostingPlan.id
siteConfig: {
linuxFxVersion: 'DOTNET-ISOLATED|8.0'
appSettings: [
{ name: 'FUNCTIONS_EXTENSION_VERSION', value: '~4' }
{ name: 'FUNCTIONS_WORKER_RUNTIME', value: 'dotnet-isolated' }
{ name: 'AzureWebJobsStorage__accountName', value: storageAccount.name }
{ name: 'WEBSITE_CONTENTAZUREFILECONNECTIONSTRING__accountName', value: storageAccount.name }
{ name: 'WEBSITE_CONTENTSHARE', value: functionAppName }
{ name: 'APPLICATIONINSIGHTS_CONNECTION_STRING', value: appInsights.properties.ConnectionString }
{ name: 'APPLICATIONINSIGHTS_AUTHENTICATION_STRING', value: 'Authorization=AAD' }
]
}
}
identity: {
type: 'SystemAssigned'
}
}
```


**Flex Consumption plan (after):**

```
// Flex Consumption plan (required)
resource hostingPlan 'Microsoft.Web/serverfarms@2023-12-01' = {
name: hostingPlanName
location: location
sku: {
name: 'FC1'
tier: 'FlexConsumption'
}
kind: 'functionapp'
properties: {
reserved: true
}
}
// Deployment storage container (required)
resource deploymentContainer 'Microsoft.Storage/storageAccounts/blobServices/containers@2023-05-01' = {
name: '${storageAccount.name}/default/deployments'
}
resource functionApp 'Microsoft.Web/sites@2023-12-01' = {
name: functionAppName
location: location
kind: 'functionapp,linux'
properties: {
serverFarmId: hostingPlan.id
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storageAccount.properties.primaryEndpoints.blob}deployments'
authentication: {
type: 'SystemAssignedIdentity'
}
}
}
scaleAndConcurrency: {
maximumInstanceCount: 100
instanceMemoryMB: 2048
}
runtime: {
name: 'dotnet-isolated'
version: '8.0'
}
}
siteConfig: {
appSettings: [
{ name: 'AzureWebJobsStorage__accountName', value: storageAccount.name }
{ name: 'APPLICATIONINSIGHTS_CONNECTION_STRING', value: appInsights.properties.ConnectionString }
{ name: 'APPLICATIONINSIGHTS_AUTHENTICATION_STRING', value: 'Authorization=AAD' }
]
}
}
identity: {
type: 'SystemAssigned'
}
}
```


Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

with `Authorization=AAD`

, you must also assign the **Monitoring Metrics Publisher** role to the function app's managed identity on the Application Insights resource.

For complete Bicep examples, see the [Flex Consumption Bicep samples](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples/tree/main/IaC/bicep).

#### Reconciling IaC after migration

If you use Infrastructure as Code (IaC) to manage your Azure resources, you need to update your IaC files after migrating to Flex Consumption to prevent configuration drift. Here's a recommended approach:

**Don't mix manual and IaC deployments**: If you used the Azure CLI or portal to create your Flex Consumption app during migration, update your IaC files before the next deployment. Otherwise, your IaC might attempt to recreate the old Consumption plan resources.**Update resource names or use lifecycle management**: Since you can't convert a Consumption app to Flex Consumption in place, you have two options:**New resource names**: Update your IaC to use new names for the hosting plan and function app. This approach keeps your old resources intact until you're confident the migration succeeded.**Import existing resources**: If you want to keep the same names, delete the old resources first, then let your IaC create the new Flex Consumption resources. Alternatively, import the manually-created resources into your Terraform state using`terraform import`

or reference existing resources in Bicep.

**Verify state alignment**: After updating your IaC files, run a plan/preview operation (`terraform plan`

or`az deployment group what-if`

) to confirm no unexpected changes will occur.**Update CI/CD pipelines**: If your deployment pipelines reference the old Consumption plan configuration, update them to use the new Flex Consumption resource definitions and deployment methods.

Tip

To minimize disruption, consider running both the old Consumption app and new Flex Consumption app in parallel during a transition period. Update your IaC to manage the new Flex Consumption app, verify it works correctly, then remove the old Consumption app resources from both Azure and your IaC files.

### Remove the original app (optional)

After thoroughly testing your new Flex Consumption function app and validating that everything is working as expected, you might want to clean up resources to avoid unnecessary costs. Even though triggers in the original app are likely already disabled, you might wait a few days or even weeks before removing the original app entirely. This delay, which depends on your application's usage patterns, makes sure that all scenarios, including infrequent ones, are properly tested. Only after you're satisfied with the migration results, should you proceed to remove your original function app.

Important

This action deletes your original function app. The Consumption plan remains intact if other apps are using it. Before you proceed, make sure you've successfully migrated all functionality to the new Flex Consumption app, verified no traffic is being directed to the original app, and backed up any relevant logs, configuration, or data that might be needed for reference.

Use the [ az functionapp delete](/en-us/cli/azure/functionapp#az-functionapp-delete) command to delete the original function app:

```
az functionapp delete --name <ORIGINAL_APP_NAME> --resource-group <RESOURCE_GROUP>
```


In this example, replace `<RESOURCE_GROUP>`

and `<APP_NAME>`

with your resource group and function app names, respectively.

## Troubleshooting and Recovery Strategies

Despite careful planning, migration issues can occur. Here's how to handle potential issues during migration:

| Issue | Solution |
|---|---|
| Cold start performance issues | • Review
• Check for missing dependencies |

[extension bundles](../extension-bundles)• Update binding configurations

[Application Insights connection](../configure-monitoring#enable-application-insights-integration)[General troubleshooting steps](#general-troubleshooting-steps)[General troubleshooting steps](#general-troubleshooting-steps)If you experience issues migrating a production app, you might want to [rollback the migration to the original app](#rollback-steps-for-critical-production-apps) while you troubleshoot.

### General troubleshooting steps

Use these steps for cases where the new app fails to start or function triggers aren't processing events:

In your new app page in the

[Azure portal](https://portal.azure.com), select**Diagnose and solve problems**in the left pane of the app page. Select**Availability and Performance**and review the**Function App Down or Reporting Errors**detector. For more information, see[Azure Functions diagnostics overview](../functions-diagnostics).In the app page, select

**Monitoring**>**Application Insights**>**View Application Insights data**then select**Investigate**>**Failures**and check for any failure events.Select

**Monitoring**>**Logs**and run this Kusto query to check these tables for errors:`traces | where severityLevel == 3 | where cloud_RoleName == "<APP_NAME>" | where timestamp > ago(1d) | project timestamp, message, operation_Name, customDimensions | order by timestamp desc`

In these queries, replace

`<APP_NAME>`

with the name of your new app. These queries check for errors in the past day (`where timestamp > ago(1d)`

).Back in the app page, select

**Settings**>**Environment variables**and verify that all critical application settings were correctly transferred. Look for any[deprecated settings](../functions-app-settings#flex-consumption-plan-deprecations)that might have been incorrectly migrated or any typos or incorrect connection strings. Verify the[default host storage connection](../functions-recover-storage-account).Select

**Settings**>**Identity**and double-check that the expected identities exist and that they have been assigned to the correct roles.In your code, verify that all binding configurations are correct, paying particular attention to connection string names, storage queue and container names, and consumer group settings in Event Hubs triggers.


### Rollback steps for critical production apps

If you aren't able to troubleshoot successfully, you might want to revert to using your original app while you continue to troubleshoot.

If the original app was stopped, restart it:

Use this

command to restart the original function app:`az functionapp start`

`az functionapp delete --name <ORIGINAL_APP_NAME> --resource-group <RESOURCE_GROUP>`

If you created new queues/topics/containers, ensure clients are redirected back to the original resources.

If you modified DNS or custom domains, revert these changes to point to the original app.


## Providing feedback

If you encounter issues with your migration using this article or want to provide other feedback on this guidance, use one of these methods to get help or provide your feedback:

-[Get help at Microsoft Q&A](/en-us/answers/tags/87/azure-functions/)

-Create an issue in the [Azure Functions repo](https://github.com/Azure/Azure-Functions/issues)

-[Provide product feedback](https://feedback.azure.com/d365community/forum/9df02822-f224-ec11-b6e6-000d3a4f0da0)

-[Create a support ticket](https://azure.microsoft.com/support/create-ticket)
