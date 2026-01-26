---
merged_at: 2026-01-26T23:29:57.721909
merged_files: 2
---


---
<!-- Source: N/A -->

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
<!-- Source: N/A -->

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
