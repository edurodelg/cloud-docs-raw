---
merged_at: 2026-01-26T23:29:57.716291
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-other -->

# Quickstart: Create and deploy function code to Azure using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Visual Studio Code to create a function that responds to HTTP requests from a template. Use GitHub Copilot to improve the generated function code, verify code updates locally, and then deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Use Visual Studio Code to create a [custom handler](functions-custom-handlers) function that responds to HTTP requests. After verifying the code locally, you deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Custom handlers can be used to create functions in any language or runtime by running an HTTP server process. This article supports both Go and Rust.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17, or 21 (Linux-only).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Install or update Core Tools

The Azure Functions extension for Visual Studio Code integrates with Azure Functions Core Tools so that you can run and debug your functions locally in Visual Studio Code using the Azure Functions runtime. Before getting started, it's a good idea to install Core Tools locally or update an existing installation to use the latest version.

In Visual Studio Code, select F1 to open the command palette, and then search for and run the command **Azure Functions: Install or Update Core Tools**.

This command tries to either start a package-based installation of the latest version of Core Tools or update an existing package-based installation. If you don't have npm or Homebrew installed on your local computer, you must instead [manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in your preferred language. Later in the article, you update, run, and then publish your function code to Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.Provide the following information at the prompts:

Prompt Selection **Select a language**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Java`

.**Select a version of Java**Choose `Java 8`

,`Java 11`

,`Java 17`

or`Java 21`

, the Java version on which your functions run in Azure. Choose a Java version that you've verified locally.**Provide a group ID**Choose `com.function`

.**Provide an artifact ID**Choose `myFunction`

.**Provide a version**Choose `1.0-SNAPSHOT`

.**Provide a package name**Choose `com.function`

.**Provide an app name**Choose `myFunction-12345`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Select the build tool for Java project**Choose `Maven`

.**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `JavaScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `TypeScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `HTTP trigger`

.**Name of the function you want to create**Enter `HttpExample`

.**Authorization level**Choose `FUNCTION`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `PowerShell`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `Custom Handler`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Using this information, Visual Studio Code generates a code project for Azure Functions with an HTTP trigger function endpoint. You can view the local project files in the Explorer. To learn more about files that are created, see

[Generated project files](functions-develop-vs-code?tabs=javascript#generated-project-files).

In the local.settings.json file, update the

`AzureWebJobsStorage`

setting as in the following example:`"AzureWebJobsStorage": "UseDevelopmentStorage=true",`

This setting tells the local Functions host to use the storage emulator for the storage connection required by the Python v2 model. When you publish your project to Azure, this setting uses the default storage account instead. If you use an Azure Storage account during local development, set your storage account connection string here.


## Start the emulator

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run your function locally.


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

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the Output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, choose the Azure icon in the activity bar. In the**Workspace**area, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the new function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.With the

**Terminal**panel focused, press`Ctrl + C`to stop Core Tools and disconnect the debugger.

After you verify that the function runs correctly on your local computer, you can optionally use AI tools, such as GitHub Copilot in Visual Studio Code, to update template-generated function code.

## Use AI to normalize and validate input

This example prompt for Copilot Chat updates the existing function code to retrieve parameters from either the query string or JSON body. It applies formatting or type conversions and returns the parameters as JSON in the response:

```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Make sure that any added packages are compatible with the version of the packages already in the project
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Update the FunctionTest.java file to test the new logic.
```


You can customize your prompt to add specifics as needed. Then run the app again locally and verify that it works as expected after the code changes. This time, use a message body like:

```
{ "name": "devon torres", "email": "torres.devon@contoso.com", "age": "34" }
```


Tip

GitHub Copilot is powered by AI, so surprises and mistakes are possible. If you encounter any errors during execution, paste the error message in the chat window, select **Agent** mode, and ask Copilot to help resolve the error. For more information, see [Copilot FAQs](https://aka.ms/copilot-general-use-faqs).

When running in **Agent** mode, the results of this customization depend on the specific tools available to your agent.

When you're satisfied with your app, use Visual Studio Code to publish the project directly to Azure.

After you verify that the function runs correctly on your local computer, use Visual Studio Code to publish the project directly to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Compile the custom handler for Azure

In this section, you compile your project for deployment to Azure in a function app running Linux. In most cases, you need to recompile your binary and adjust your configuration to match the target platform before publishing it to Azure.

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Run the function in Azure

Press

`F1`to display the command palette, then search for and run the command`Azure Functions:Execute Function Now...`

. If prompted, select your subscription.Select your new function app resource and

`HttpExample`

as your function.In

**Enter request body**type`{ "name": "Contoso", "email": "me@contoso.com", "age": "34" }`

, then press Enter to send this request message to your function.When the function executes in Azure, the response is displayed in the notification area. Expand the notification to review the full response.


## Troubleshooting

Use the following table to resolve the most common issues encountered when using this article.

| Problem | Solution |
|---|---|
| Can't create a local function project? | Make sure you have the
|

[Azure Functions Core Tools installed](functions-run-local?tabs=node).When running on Windows, make sure that the default terminal shell for Visual Studio Code isn't set to WSL Bash.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

- In Visual Studio Code, select the Azure icon to open the Azure explorer.
- In the Resource Groups section, find your resource group.
- Right-click the resource group and select
**Delete**.

To learn more about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

## Next steps

You used [Visual Studio Code](functions-develop-vs-code) to create a function app with a simple HTTP-triggered function. In the next articles, you expand that function by connecting to either Azure Cosmos DB or Azure Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function). If you want to learn more about security, see [Securing Azure Functions](security-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-python -->

# Quickstart: Create and deploy function code to Azure using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Visual Studio Code to create a function that responds to HTTP requests from a template. Use GitHub Copilot to improve the generated function code, verify code updates locally, and then deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Use Visual Studio Code to create a [custom handler](functions-custom-handlers) function that responds to HTTP requests. After verifying the code locally, you deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Custom handlers can be used to create functions in any language or runtime by running an HTTP server process. This article supports both Go and Rust.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17, or 21 (Linux-only).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Install or update Core Tools

The Azure Functions extension for Visual Studio Code integrates with Azure Functions Core Tools so that you can run and debug your functions locally in Visual Studio Code using the Azure Functions runtime. Before getting started, it's a good idea to install Core Tools locally or update an existing installation to use the latest version.

In Visual Studio Code, select F1 to open the command palette, and then search for and run the command **Azure Functions: Install or Update Core Tools**.

This command tries to either start a package-based installation of the latest version of Core Tools or update an existing package-based installation. If you don't have npm or Homebrew installed on your local computer, you must instead [manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in your preferred language. Later in the article, you update, run, and then publish your function code to Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.Provide the following information at the prompts:

Prompt Selection **Select a language**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Java`

.**Select a version of Java**Choose `Java 8`

,`Java 11`

,`Java 17`

or`Java 21`

, the Java version on which your functions run in Azure. Choose a Java version that you've verified locally.**Provide a group ID**Choose `com.function`

.**Provide an artifact ID**Choose `myFunction`

.**Provide a version**Choose `1.0-SNAPSHOT`

.**Provide a package name**Choose `com.function`

.**Provide an app name**Choose `myFunction-12345`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Select the build tool for Java project**Choose `Maven`

.**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `JavaScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `TypeScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `HTTP trigger`

.**Name of the function you want to create**Enter `HttpExample`

.**Authorization level**Choose `FUNCTION`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `PowerShell`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `Custom Handler`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Using this information, Visual Studio Code generates a code project for Azure Functions with an HTTP trigger function endpoint. You can view the local project files in the Explorer. To learn more about files that are created, see

[Generated project files](functions-develop-vs-code?tabs=javascript#generated-project-files).

In the local.settings.json file, update the

`AzureWebJobsStorage`

setting as in the following example:`"AzureWebJobsStorage": "UseDevelopmentStorage=true",`

This setting tells the local Functions host to use the storage emulator for the storage connection required by the Python v2 model. When you publish your project to Azure, this setting uses the default storage account instead. If you use an Azure Storage account during local development, set your storage account connection string here.


## Start the emulator

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run your function locally.


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

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the Output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, choose the Azure icon in the activity bar. In the**Workspace**area, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the new function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.With the

**Terminal**panel focused, press`Ctrl + C`to stop Core Tools and disconnect the debugger.

After you verify that the function runs correctly on your local computer, you can optionally use AI tools, such as GitHub Copilot in Visual Studio Code, to update template-generated function code.

## Use AI to normalize and validate input

This example prompt for Copilot Chat updates the existing function code to retrieve parameters from either the query string or JSON body. It applies formatting or type conversions and returns the parameters as JSON in the response:

```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Make sure that any added packages are compatible with the version of the packages already in the project
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Update the FunctionTest.java file to test the new logic.
```


You can customize your prompt to add specifics as needed. Then run the app again locally and verify that it works as expected after the code changes. This time, use a message body like:

```
{ "name": "devon torres", "email": "torres.devon@contoso.com", "age": "34" }
```


Tip

GitHub Copilot is powered by AI, so surprises and mistakes are possible. If you encounter any errors during execution, paste the error message in the chat window, select **Agent** mode, and ask Copilot to help resolve the error. For more information, see [Copilot FAQs](https://aka.ms/copilot-general-use-faqs).

When running in **Agent** mode, the results of this customization depend on the specific tools available to your agent.

When you're satisfied with your app, use Visual Studio Code to publish the project directly to Azure.

After you verify that the function runs correctly on your local computer, use Visual Studio Code to publish the project directly to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Compile the custom handler for Azure

In this section, you compile your project for deployment to Azure in a function app running Linux. In most cases, you need to recompile your binary and adjust your configuration to match the target platform before publishing it to Azure.

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Run the function in Azure

Press

`F1`to display the command palette, then search for and run the command`Azure Functions:Execute Function Now...`

. If prompted, select your subscription.Select your new function app resource and

`HttpExample`

as your function.In

**Enter request body**type`{ "name": "Contoso", "email": "me@contoso.com", "age": "34" }`

, then press Enter to send this request message to your function.When the function executes in Azure, the response is displayed in the notification area. Expand the notification to review the full response.


## Troubleshooting

Use the following table to resolve the most common issues encountered when using this article.

| Problem | Solution |
|---|---|
| Can't create a local function project? | Make sure you have the
|

[Azure Functions Core Tools installed](functions-run-local?tabs=node).When running on Windows, make sure that the default terminal shell for Visual Studio Code isn't set to WSL Bash.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

- In Visual Studio Code, select the Azure icon to open the Azure explorer.
- In the Resource Groups section, find your resource group.
- Right-click the resource group and select
**Delete**.

To learn more about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

## Next steps

You used [Visual Studio Code](functions-develop-vs-code) to create a function app with a simple HTTP-triggered function. In the next articles, you expand that function by connecting to either Azure Cosmos DB or Azure Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function). If you want to learn more about security, see [Securing Azure Functions](security-concepts).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-output -->

# Azure Service Bus output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Service Bus output binding to send queue or topic messages.

For information on setup and configuration details, see the [overview](functions-bindings-service-bus).

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

This code defines and initializes the `ILogger`

:

```
private readonly ILogger<ServiceBusReceivedMessageFunctions> _logger;
public ServiceBusReceivedMessageFunctions(ILogger<ServiceBusReceivedMessageFunctions> logger)
{
_logger = logger;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives a message and writes it to a second queue:

```
[Function(nameof(ServiceBusReceivedMessageFunction))]
[ServiceBusOutput("outputQueue", Connection = "ServiceBusConnection")]
public string ServiceBusReceivedMessageFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection")] ServiceBusReceivedMessage message)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
var outputMessage = $"Output message created at {DateTime.Now}";
return outputMessage;
}
```


This example uses an HTTP trigger with an `OutputType`

object to both send an HTTP response and write the output message.

```
[Function("HttpSendMsg")]
public async Task<OutputType> Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req, FunctionContext context)
{
_logger.LogInformation($"C# HTTP trigger function processed a request for {context.InvocationId}.");
HttpResponseData response = req.CreateResponse(HttpStatusCode.OK);
await response.WriteStringAsync("HTTP response: Message sent");
return new OutputType()
{
OutputEvent = "MyMessage",
HttpResponse = response
};
}
```


This code defines the multiple output type `OutputType`

, which includes the Service Bus output binding definition on `OutputEvent`

:

```
public class OutputType
{
[ServiceBusOutput("TopicOrQueueName", Connection = "ServiceBusConnection")]
public string OutputEvent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following example shows a Java function that sends a message to a Service Bus queue `myqueue`

when triggered by an HTTP request.

```
@FunctionName("httpToServiceBusQueue")
@ServiceBusQueueOutput(name = "message", queueName = "myqueue", connection = "AzureServiceBusConnection")
public String pushToQueue(
@HttpTrigger(name = "request", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
final String message,
@HttpOutput(name = "response") final OutputBinding<T> result ) {
result.setValue(message + " has been sent.");
return message;
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@QueueOutput`

annotation on function parameters whose value would be written to a Service Bus queue. The parameter type should be `OutputBinding<T>`

, where `T`

is any native Java type of a plan old Java object (POJO).

Java functions can also write to a Service Bus topic. The following example uses the `@ServiceBusTopicOutput`

annotation to describe the configuration for the output binding.

```
@FunctionName("sbtopicsend")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@ServiceBusTopicOutput(name = "message", topicName = "mytopicname", subscriptionName = "mysubscription", connection = "ServiceBusConnection") OutputBinding<String> message,
final ExecutionContext context) {
String name = request.getBody().orElse("Azure Functions");
message.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that sends a queue message every 5 minutes.

```
import { app, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<string> {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.serviceBusQueue({
queueName: 'testqueue',
connection: 'MyServiceBusConnection',
}),
handler: timerTrigger1,
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that sends a queue message every 5 minutes.

```
const { app, output } = require('@azure/functions');
const serviceBusOutput = output.serviceBusQueue({
queueName: 'testqueue',
connection: 'MyServiceBusConnection',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: serviceBusOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
},
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a Service Bus output binding in a *function.json* file and a [PowerShell function](functions-reference-powershell) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "serviceBus",
"direction": "out",
"connection": "AzureServiceBusConnectionString",
"name": "outputSbMsg",
"queueName": "outqueue",
"topicName": "outtopic"
}
]
}
```


Here's the PowerShell that creates a message as the function's output.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name outputSbMsg -Value @{
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write out to a Service Bus topics and Service Bus queues in Python. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

This example shows how to write out to a Service Bus topic.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route(route="put_message")
@app.service_bus_topic_output(arg_name="message",
connection="AzureServiceBusConnectionString",
topic_name="outTopic")
def main(req: func.HttpRequest, message: func.Out[str]) -> func.HttpResponse:
input_msg = req.params.get('message')
message.set(input_msg)
return 'OK'
```


This example shows how to write out to a Service Bus queue.

```
import azure.functions as func
app = func.FunctionApp()
@app.route(route="put_message")
@app.service_bus_queue_output(
arg_name="msg",
connection="AzureServiceBusConnectionString",
queue_name="outqueue")
def put_message(req: func.HttpRequest, msg: func.Out[str]):
msg.set(req.get_body().decode('utf-8'))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#service-bus-output).

In [C# class libraries](dotnet-isolated-process-guide), use the [ServiceBusOutputAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.ServiceBus/src/ServiceBusOutputAttribute.cs) to define the queue or topic written to by the output.

The following table explains the properties you can set using the attribute:

| Property | Description |
|---|---|
EntityType |
Sets the entity type as either `Queue` for sending messages to a queue or `Topic` when sending messages to a topic. |
QueueOrTopicName |
Name of the topic or queue to send messages to. Use `EntityType` to set the destination type. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `service_bus_topic_output`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the queue or topic message in function code. |
`queue_name` |
Name of the queue. Set only if sending queue messages, not for a topic. |
`topic_name` |
Name of the topic. Set only if sending topic messages, not for a queue. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `ServiceBusQueueOutput`

and `ServiceBusTopicOutput`

annotations are available to write a message as a function output. The parameter decorated with these annotations must be declared as an `OutputBinding<T>`

where `T`

is the type corresponding to the message's type.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.serviceBusQueue()`

method.

| Property | Description |
|---|---|
queueName |
Name of the queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

The following table explains the properties that you can set on the `options`

object passed to the `output.serviceBusTopic()`

method.

| Property | Description |
|---|---|
topicName |
Name of the topic. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

The following table explains the binding configuration properties that you set in the *function.json* file and the `ServiceBus`

attribute.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBus` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. Set to "$return" to reference the function return value. |
queueName |
Name of the queue. Set only if sending queue messages, not for a topic. |
topicName |
Name of the topic. Set only if sending topic messages, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**(v1 only)`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that doesn't have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property isn't available because the latest version of the Service Bus SDK doesn't support manage operations.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

All C# modalities and extension versions support the following output parameter types:

| Type | Description |
|---|---|
|
Use when the message to write is simple text. When the parameter value is null when the function exits, Functions doesn't create a message. |
byte[] |
Use for writing binary data messages. When the parameter value is null when the function exits, Functions doesn't create a message. |
Object |
When a message contains JSON, Functions serializes the object into a JSON message payload. When the parameter value is null when the function exits, Functions creates a message with a null object. |

Messaging-specific parameter types contain extra message metadata and aren't compatible with JSON serialization. As a result, it isn't possible to use `ServiceBusMessage`

with the output binding in the isolated model. The specific types supported by the output binding depend on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single message, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | An object representing the message. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple messages, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array containing multiple message. Each entry represents one message. |

For other output scenarios, create and use a [ServiceBusClient](/en-us/dotnet/api/azure.messaging.servicebus.servicebusclient) with other types from [Azure.Messaging.ServiceBus](/en-us/dotnet/api/azure.messaging.servicebus) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

In Azure Functions 1.x, the runtime creates the queue if it doesn't exist and you have set `accessRights`

to `manage`

. In Azure Functions version 2.x and higher, the queue or topic must already exist; if you specify a queue or topic that doesn't exist, the function fails.

Use the [Azure Service Bus SDK](../service-bus-messaging/) rather than the built-in output binding.

Output to the Service Bus is available via the `Push-OutputBinding`

cmdlet where you pass arguments that match the name designated by binding's name parameter in the *function.json* file.

The output function parameter must be defined as `func.Out[str]`

or `func.Out[bytes]`

. Refer to the [output example](#example) for details.
Alternatively, you can use the [Azure Service Bus SDK](../service-bus-messaging/) rather than the built-in output binding.

For a complete example, see [the examples section](#example).

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Service Bus. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Get the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues#get-the-connection-string). The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name. For example, if you set `connection`

to "MyServiceBus", the Functions runtime looks for an app setting that is named "AzureWebJobsMyServiceBus". If you leave `connection`

empty, the Functions runtime uses the default Service Bus connection string in the app setting that is named "AzureWebJobsServiceBus".

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-service-bus?extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Service Bus namespace. | <service_bus_namespace>.servicebus.windows.net |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your topics and queues at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Service Bus extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
Trigger1 |
|

[Azure Service Bus Data Sender](../role-based-access-control/built-in-roles#azure-service-bus-data-sender)1 For triggering from Service Bus topics, the role assignment needs to have effective scope over the Service Bus subscription resource. If only the topic is included, an error will occur. Some clients, such as the Azure portal, don't expose the Service Bus subscription resource as a scope for role assignment. In such cases, the Azure CLI may be used instead. To learn more, see [Azure built-in roles for Azure Service Bus](../service-bus-messaging/service-bus-managed-service-identity#resource-scope).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Service Bus |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs -->

# Azure Event Hubs trigger and bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with [Azure Event Hubs](../event-hubs/event-hubs-about) bindings for Azure Functions. Azure Functions supports trigger and output bindings for Event Hubs.

| Action | Type |
|---|---|
| Respond to events sent to an event hub event stream. |
|

[Output binding](functions-bindings-event-hubs-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs), version 6.x.

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

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following options:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Messaging.EventHubs] is in preview.

**Event Hubs trigger**

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Hubs output binding**

When you want the function to write a single event, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | An object representing the event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventHubProducerClient](/en-us/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) with other types from [Azure.Messaging.EventHubs](/en-us/dotnet/api/azure.messaging.eventhubs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure EventHub are in Preview. Follow the [Python SDK Bindings for EventHub Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python) to get started with SDK Types for Event Hubs in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| EventHub trigger |
|

`EventData`

## host.json settings

The [host.json](functions-host-json#eventhub) file contains settings that control behavior for the Event Hubs trigger. The configuration is different depending on the extension version.

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100,
"minEventBatchSize" : 25,
"maxWaitTime" : "00:05:00",
"batchCheckpointFrequency" : 1,
"prefetchCount" : 300,
"transportType" : "amqpWebSockets",
"webProxy" : "https://proxyserver:8080",
"customEndpointAddress" : "amqps://company.gateway.local",
"targetUnprocessedEventThreshold" : 75,
"initialOffsetOptions" : {
"type" : "fromStart",
"enqueuedTimeUtc" : ""
},
"clientRetryOptions":{
"mode" : "exponential",
"tryTimeout" : "00:01:00",
"delay" : "00:00:00.80",
"maximumDelay" : "00:01:00",
"maximumRetries" : 3
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
maxEventBatchSize2 |
100 | The maximum number of events included in a batch for a single invocation. Must be at least 1. |
minEventBatchSize1 |
1 | The minimum number of events desired in a batch. The minimum applies only when the function is receiving multiple events and must be less than `maxEventBatchSize` .The minimum size isn't strictly guaranteed. A partial batch is dispatched when a full batch can't be prepared before the `maxWaitTime` has elapsed. Partial batches are also likely for the first invocation of the function after scaling takes place. |
maxWaitTime1 |
00:01:00 | The maximum interval that the trigger should wait to fill a batch before invoking the function. The wait time is only considered when `minEventBatchSize` is larger than 1 and is otherwise ignored. If less than `minEventBatchSize` events were available before the wait time elapses, the function is invoked with a partial batch. The longest allowed wait time is 10 minutes.NOTE: This interval is not a strict guarantee for the exact timing on which the function is invoked. There is a small margin of error due to timer precision. When scaling takes place, the first invocation with a partial batch may occur more quickly or may take up to twice the configured wait time. |
| batchCheckpointFrequency | 1 | The number of batches to process before creating a checkpoint for the event hub.NOTE: Setting this value above 1 for hosting plans supported by
|
| prefetchCount | 300 | The number of events that is eagerly requested from Event Hubs and held in a local cache to allow reads to avoid waiting on a network operation |
| transportType | amqpTcp | The protocol and transport that is used for communicating with Event Hubs. Available options: `amqpTcp` , `amqpWebSockets` |
| webProxy | null | The proxy to use for communicating with Event Hubs over web sockets. A proxy cannot be used with the `amqpTcp` transport. |
| customEndpointAddress | null | The address to use when establishing a connection to Event Hubs, allowing network requests to be routed through an application gateway or other path needed for the host environment. The fully qualified namespace for the event hub is still needed when a custom endpoint address is used, and it must be specified explicitly or via the connection string. |
targetUnprocessedEventThreshold1 |
null | The desired number of unprocessed events per function instance. The threshold is used in target-based scaling to override the default scaling threshold inferred from the `maxEventBatchSize` option. When set, the total unprocessed event count is divided by this value to determine the number of function instances needed. The instance count is rounded up to a number that creates a balanced partition distribution. |
| initialOffsetOptions/type | fromStart | The location in the event stream to start processing when a checkpoint does not exist in storage. Applies to all partitions. For more information, see the
`fromStart` , `fromEnd` , `fromEnqueuedTime` |

`initialOffsetOptions/type`

is configured as `fromEnqueuedTime`

, this setting is mandatory. Supports time in any format supported by [DateTime.Parse()](/en-us/dotnet/standard/base-types/parsing-datetime), such as`2020-10-26T20:31Z`

. For clarity, you should also specify a timezone. When timezone isn't specified, Functions assumes the local timezone of the machine running the function app, which is UTC when running on Azure.`exponential`

, `fixed`

1 Using `minEventBatchSize`

and `maxWaitTime`

requires [v5.3.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/5.3.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package, or a later version.

2 The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this was 10.

The `clientRetryOptions`

are used to retry operations between the Functions host and Event Hubs (such as fetching events and sending events). Refer to guidance on [Azure Functions error handling and retries](functions-bindings-error-pages#retries) for information on applying retry policies to individual functions.

For a reference of host.json in Azure Functions 2.x and beyond, see [host.json reference for Azure Functions](functions-host-json).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot -->

# Azure IoT Hub bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with Azure Functions bindings for IoT Hub. The IoT Hub support is based on the [Azure Event Hubs Binding](functions-bindings-event-hubs).

Important

While the following code samples use the Event Hub API, the given syntax is applicable for IoT Hub functions.

| Action | Type |
|---|---|
| Respond to events sent to an IoT hub event stream. |
|

## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs), version 6.x.

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

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following options:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Messaging.EventHubs] is in preview.

**Event Hubs trigger**

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Hubs output binding**

When you want the function to write a single event, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | An object representing the event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventHubProducerClient](/en-us/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) with other types from [Azure.Messaging.EventHubs](/en-us/dotnet/api/azure.messaging.eventhubs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure EventHub are in Preview. Follow the [Python SDK Bindings for EventHub Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python) to get started with SDK Types for Event Hubs in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| EventHub trigger |
|

`EventData`

## host.json settings

The [host.json](functions-host-json#eventhub) file contains settings that control behavior for the Event Hubs trigger. The configuration is different depending on the extension version.

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100,
"minEventBatchSize" : 25,
"maxWaitTime" : "00:05:00",
"batchCheckpointFrequency" : 1,
"prefetchCount" : 300,
"transportType" : "amqpWebSockets",
"webProxy" : "https://proxyserver:8080",
"customEndpointAddress" : "amqps://company.gateway.local",
"targetUnprocessedEventThreshold" : 75,
"initialOffsetOptions" : {
"type" : "fromStart",
"enqueuedTimeUtc" : ""
},
"clientRetryOptions":{
"mode" : "exponential",
"tryTimeout" : "00:01:00",
"delay" : "00:00:00.80",
"maximumDelay" : "00:01:00",
"maximumRetries" : 3
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
maxEventBatchSize2 |
100 | The maximum number of events included in a batch for a single invocation. Must be at least 1. |
minEventBatchSize1 |
1 | The minimum number of events desired in a batch. The minimum applies only when the function is receiving multiple events and must be less than `maxEventBatchSize` .The minimum size isn't strictly guaranteed. A partial batch is dispatched when a full batch can't be prepared before the `maxWaitTime` has elapsed. Partial batches are also likely for the first invocation of the function after scaling takes place. |
maxWaitTime1 |
00:01:00 | The maximum interval that the trigger should wait to fill a batch before invoking the function. The wait time is only considered when `minEventBatchSize` is larger than 1 and is otherwise ignored. If less than `minEventBatchSize` events were available before the wait time elapses, the function is invoked with a partial batch. The longest allowed wait time is 10 minutes.NOTE: This interval is not a strict guarantee for the exact timing on which the function is invoked. There is a small margin of error due to timer precision. When scaling takes place, the first invocation with a partial batch may occur more quickly or may take up to twice the configured wait time. |
| batchCheckpointFrequency | 1 | The number of batches to process before creating a checkpoint for the event hub.NOTE: Setting this value above 1 for hosting plans supported by
|
| prefetchCount | 300 | The number of events that is eagerly requested from Event Hubs and held in a local cache to allow reads to avoid waiting on a network operation |
| transportType | amqpTcp | The protocol and transport that is used for communicating with Event Hubs. Available options: `amqpTcp` , `amqpWebSockets` |
| webProxy | null | The proxy to use for communicating with Event Hubs over web sockets. A proxy cannot be used with the `amqpTcp` transport. |
| customEndpointAddress | null | The address to use when establishing a connection to Event Hubs, allowing network requests to be routed through an application gateway or other path needed for the host environment. The fully qualified namespace for the event hub is still needed when a custom endpoint address is used, and it must be specified explicitly or via the connection string. |
targetUnprocessedEventThreshold1 |
null | The desired number of unprocessed events per function instance. The threshold is used in target-based scaling to override the default scaling threshold inferred from the `maxEventBatchSize` option. When set, the total unprocessed event count is divided by this value to determine the number of function instances needed. The instance count is rounded up to a number that creates a balanced partition distribution. |
| initialOffsetOptions/type | fromStart | The location in the event stream to start processing when a checkpoint does not exist in storage. Applies to all partitions. For more information, see the
`fromStart` , `fromEnd` , `fromEnqueuedTime` |

`initialOffsetOptions/type`

is configured as `fromEnqueuedTime`

, this setting is mandatory. Supports time in any format supported by [DateTime.Parse()](/en-us/dotnet/standard/base-types/parsing-datetime), such as`2020-10-26T20:31Z`

. For clarity, you should also specify a timezone. When timezone isn't specified, Functions assumes the local timezone of the machine running the function app, which is UTC when running on Azure.`exponential`

, `fixed`

1 Using `minEventBatchSize`

and `maxWaitTime`

requires [v5.3.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/5.3.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package, or a later version.

2 The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this was 10.

The `clientRetryOptions`

are used to retry operations between the Functions host and Event Hubs (such as fetching events and sending events). Refer to guidance on [Azure Functions error handling and retries](functions-bindings-error-pages#retries) for information on applying retry policies to individual functions.

For a reference of host.json in Azure Functions 2.x and beyond, see [host.json reference for Azure Functions](functions-host-json).
