---
merged_at: 2026-01-28T07:43:39.522018
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

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
