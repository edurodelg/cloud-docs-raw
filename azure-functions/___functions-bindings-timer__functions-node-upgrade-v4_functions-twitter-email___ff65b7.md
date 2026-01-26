---
merged_at: 2026-01-26T21:02:36.341500
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-timer -->

# Timer trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with timer triggers in Azure Functions. A timer trigger lets you run a function on a schedule.

This is reference information for Azure Functions developers. If you're new to Azure Functions, start with the following resources:

C# developer references:


For information on how to manually run a timer-triggered function, see [Manually run a non HTTP-triggered function](functions-manually-run-non-http).

Support for this binding is automatically provided in all development environments. You don't have to manually install the package or register the extension.

Source code for the timer extension package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/) GitHub repository.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

This example shows a C# function that executes each time the minutes have a value divisible by five. For example, when the function starts at 18:55:00, the next execution is at 19:00:00. A `TimerInfo`

object is passed to the function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

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


The following example function triggers and executes every five minutes. The `@TimerTrigger`

annotation on the function defines the schedule using the same string format as [CRON expressions](https://en.wikipedia.org/wiki/Cron#CRON_expression).

```
@FunctionName("keepAlive")
public void keepAlive(
@TimerTrigger(name = "keepAliveTrigger", schedule = "0 */5 * * * *") String timerInfo,
ExecutionContext context
) {
// timeInfo is a JSON string, you can deserialize it to an object using your favorite JSON library
context.getLogger().info("Timer is triggered: " + timerInfo);
}
```


The following example shows a timer trigger binding and function code that uses the binding, where an instance representing the timer is passed to the function. The function writes a log indicating whether this function invocation is due to a missed schedule occurrence. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import datetime
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="mytimer")
@app.timer_trigger(schedule="0 */5 * * * *",
arg_name="mytimer",
run_on_startup=False)
def test_function(mytimer: func.TimerRequest) -> None:
utc_timestamp = datetime.datetime.utcnow().replace(
tzinfo=datetime.timezone.utc).isoformat()
if mytimer.past_due:
logging.info('The timer is past due!')
logging.info('Python timer trigger function ran at %s', utc_timestamp)
```


The following example shows a timer trigger [TypeScript function](functions-reference-node?tabs=typescript).

```
import { app, InvocationContext, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<void> {
context.log('Timer function processed request.');
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
handler: timerTrigger1,
});
```


The following example shows a timer trigger [JavaScript function](functions-reference-node).

Here's the binding data in the *function.json* file:

```
{
"schedule": "0 */5 * * * *",
"name": "myTimer",
"type": "timerTrigger",
"direction": "in"
}
```


The following is the timer function code in the run.ps1 file:

```
# Input bindings are passed in via param block.
param($myTimer)
# Get the current universal time in the default string format.
$currentUTCtime = (Get-Date).ToUniversalTime()
# The 'IsPastDue' property is 'true' when the current function invocation is later than scheduled.
if ($myTimer.IsPastDue) {
Write-Host "PowerShell timer is running late!"
}
# Write an information log with the current time.
Write-Host "PowerShell timer trigger function ran! TIME: $currentUTCtime"
```


## Attributes

[In-process](functions-dotnet-class-library) C# library uses [TimerTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerTriggerAttribute.cs) from [Microsoft.Azure.WebJobs.Extensions](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions) whereas [isolated worker process](dotnet-isolated-process-guide) C# library uses [TimerTriggerAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.Timer/src/TimerTriggerAttribute.cs) from [Microsoft.Azure.Functions.Worker.Extensions.Timer](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Timer) to define the function. C# script instead uses a [function.json configuration file](#configuration).

| Attribute property | Description |
|---|---|
Schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as `%ScheduleAppSetting%` . |

**RunOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***RunOnStartup**should rarely if ever be set to`true`

, especially in production.**UseMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `schedule`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the timer object in function code. |
`schedule` |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

`run_on_startup`

`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.`use_monitor`

`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@TimerTrigger`

annotation on the function defines the `schedule`

using the same string format as [CRON expressions](https://en.wikipedia.org/wiki/Cron#CRON_expression). The annotation supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.timer()`

method.

| Property | Description |
|---|---|
schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

**runOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.**useMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to "timerTrigger". This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to "in". This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the timer object in function code. |
schedule |
A
`TimeSpan` can be used only for a function app that runs on an App Service Plan. You can put the schedule expression in an app setting and set this property to the app setting name wrapped in % signs, as in this example: "%ScheduleAppSetting%". |

**runOnStartup**`true`

, the function is invoked when the runtime starts. For example, the runtime starts when the function app wakes up after going idle due to inactivity. when the function app restarts due to function changes, and when the function app scales out. *Use with caution.***runOnStartup**should rarely if ever be set to`true`

, especially in production.**useMonitor**`true`

or `false`

to indicate whether the schedule should be monitored. Schedule monitoring persists schedule occurrences to aid in ensuring the schedule is maintained correctly even when function app instances restart. If not set explicitly, the default is `true`

for schedules that have a recurrence interval greater than or equal to 1 minute. For schedules that trigger more than once per minute, the default is `false`

.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Caution

Don't set **runOnStartup** to `true`

in production. Using this setting makes code execute at highly unpredictable times. In certain production settings, these extra executions can result in significantly higher costs for apps hosted in a Consumption plan. For example, with **runOnStartup** enabled the trigger is invoked whenever your function app is scaled. Make sure you fully understand the production behavior of your functions before enabling **runOnStartup** in production.

See the [Example section](#example) for complete examples.

## Usage

When a timer trigger function is invoked, a timer object is passed into the function. The following JSON is an example representation of the timer object.

```
{
"Schedule":{
"AdjustForDST": true
},
"ScheduleStatus": {
"Last":"2016-10-04T10:15:00+00:00",
"LastUpdated":"2016-10-04T10:16:00+00:00",
"Next":"2016-10-04T10:20:00+00:00"
},
"IsPastDue":false
}
```


```
{
"schedule":{
"adjustForDST": true
},
"scheduleStatus": {
"last":"2016-10-04T10:15:00+00:00",
"lastUpdated":"2016-10-04T10:16:00+00:00",
"next":"2016-10-04T10:20:00+00:00"
},
"isPastDue":false
}
```


The `isPastDue`

property is `true`

when the current function invocation is later than scheduled. For example, a function app restart might cause an invocation to be missed.

### NCRONTAB expressions

Azure Functions uses the [NCronTab](https://github.com/atifaziz/NCrontab) library to interpret NCRONTAB expressions. An NCRONTAB expression is similar to a CRON expression except that it includes an additional sixth field at the beginning to use for time precision in seconds:

`{second} {minute} {hour} {day} {month} {day-of-week}`


Each field can have one of the following types of values:

| Type | Example | When triggered |
|---|---|---|
| A specific value | `0 5 * * * *` |
Once every hour of the day at minute 5 of each hour |
All values (`*` ) |
`0 * 5 * * *` |
At every minute in the hour, during hour 5 |
A range (`-` operator) |
`5-7 * * * * *` |
Three times a minute - at seconds 5 through 7 during every minute of every hour of each day |
A set of values (`,` operator) |
`5,8,10 * * * * *` |
Three times a minute - at seconds 5, 8, and 10 during every minute of every hour of each day |
An interval value (`/` operator) |
`0 */5 * * * *` |
12 times an hour - at second 0 of every 5th minute of every hour of each day |

To specify months or days you can use numeric values, names, or abbreviations of names:

- For days, the numeric values are 0 to 6, where 0 starts with Sunday.
- Names are in English. For example:
`Monday`

,`January`

. - Names are case-insensitive.
- Names can be abbreviated. We recommend using three letters for abbreviations. For example:
`Mon`

,`Jan`

.

#### NCRONTAB examples

Here are some examples of NCRONTAB expressions you can use for the timer trigger in Azure Functions.

| Example | When triggered |
|---|---|
`0 */5 * * * *` |
once every five minutes |
`0 0 * * * *` |
once at the top of every hour |
`0 0 */2 * * *` |
once every two hours |
`0 0 9-17 * * *` |
once every hour from 9 AM to 5 PM |
`0 30 9 * * *` |
at 9:30 AM every day |
`0 30 9 * * 1-5` |
at 9:30 AM every weekday |
`0 30 9 * Jan Mon` |
at 9:30 AM every Monday in January |

Note

NCRONTAB expression supports both **five field** and **six field** format. The sixth field position is a value for seconds which is placed at the beginning of the expression.
If the CRON expression is invalid the Azure Portal Function Test will display a 404 error, if Application Insights is connected more details are logged there.

#### NCRONTAB time zones

The numbers in an NCRONTAB expression refer to a time and date, not a time span. For example, a 5 in the `hour`

field refers to 5:00 AM, not every 5 hours.

The default time zone used with the CRON expressions is Coordinated Universal Time (UTC). To have your CRON expression based on another time zone, create an app setting for your function app named `WEBSITE_TIME_ZONE`

.

The value of this setting depends on the operating system and plan on which your function app runs.

| Operating system | Plan | Value |
|---|---|---|
Windows |
All | Set the value to the name of the desired time zone as given by the second line from each pair given by the Windows command `tzutil.exe /L` |
Linux |
Premium Dedicated |
Set the value to the name of the desired time zone as shown in the
|

Note

`WEBSITE_TIME_ZONE`

and `TZ`

aren't currently supported when running on Linux in a [Flex Consumption](flex-consumption-plan) or [Consumption](consumption-plan) plan. In this case, the setting `WEBSITE_TIME_ZONE`

or `TZ`

can create SSL-related issues and cause metrics to stop working for your app.

For example, Eastern Time in the US (represented by `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux)) currently uses UTC-05:00 during standard time and UTC-04:00 during daylight time. To have a timer trigger fire at 10:00 AM Eastern Time every day, create an app setting for your function app named `WEBSITE_TIME_ZONE`

, set the value to `Eastern Standard Time`

(Windows) or `America/New_York`

(Linux), and then use the following NCRONTAB expression:

```
"0 0 10 * * *"
```


When you use `WEBSITE_TIME_ZONE`

, the time is adjusted for time changes in the specific timezone, including daylight saving time and changes in standard time.

### TimeSpan

A `TimeSpan`

can be used only for a function app that runs on an App Service Plan.

Unlike an NCRONTAB expression, a `TimeSpan`

value specifies the time interval between each function invocation. When a function completes after running longer than the specified interval, the timer immediately invokes the function again.

Expressed as a string, the `TimeSpan`

format is `hh:mm:ss`

when `hh`

is less than 24. When the first two digits are 24 or greater, the format is `dd:hh:mm`

. Here are some examples:

| Example | When triggered |
|---|---|
| "01:00:00" | every hour |
| "00:01:00" | every minute |
| "25:00:00:00" | every 25 days |
| "1.00:00:00" | every day |

### Scale-out

If a function app scales out to multiple instances, only a single instance of a timer-triggered function is run across all instances. It will not trigger again if there is an outstanding invocation still running.

### Function apps sharing Storage

If you are sharing storage accounts across function apps that are not deployed to app service, you might need to explicitly assign host ID to each app.

| Functions version | Setting |
|---|---|
| 2.x (and higher) | `AzureFunctionsWebHost__hostid` environment variable |
| 1.x | `id` in host.json |

You can omit the identifying value or manually set each function app's identifying configuration to a different value.

The timer trigger uses a storage lock to ensure that there is only one timer instance when a function app scales out to multiple instances. If two function apps share the same identifying configuration and each uses a timer trigger, only one timer runs.

### Retry behavior

Unlike the queue trigger, the timer trigger doesn't retry after a function fails. When a function fails, it isn't called again until the next time on the schedule.

### Manually invoke a timer trigger

The timer trigger for Azure Functions provides an HTTP webhook that can be invoked to manually trigger the function. This can be extremely useful in the following scenarios.

- Integration testing
- Slot swaps as part of a smoke test or warmup activity
- Initial deployment of a function to immediately populate a cache or lookup table in a database

Please refer to [manually run a non HTTP-triggered function](functions-manually-run-non-http) for details on how to manually invoke a timer triggered function.

### Troubleshooting

For information about what to do when the timer trigger doesn't work as expected, see [Investigating and reporting issues with timer triggered functions not firing](https://github.com/Azure/azure-functions-host/wiki/Investigating-and-reporting-issues-with-timer-triggered-functions-not-firing).

## Connections

Timer triggers have an implicit dependency on blob storage, except when run locally through the Azure Functions Core Tools. The system uses blob storage to coordinate across multiple instances [when the app scales out](#scale-out). It accesses blob storage using the host storage (`AzureWebJobsStorage`

) connection. If you configure the host storage to use an [identity-based connection](functions-reference#connecting-to-host-storage-with-an-identity), the identity should have the [Storage Blob Data Owner](../role-based-access-control/built-in-roles#storage-blob-data-owner) role, which is the default requirement for host storage.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-node-upgrade-v4 -->

# Migrate to version 4 of the Node.js programming model for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article discusses the differences between version 3 and version 4 of the Node.js programming model and how to upgrade an existing v3 app. If you want to create a new v4 app instead of upgrading an existing v3 app, see the tutorial for either [Visual Studio Code (VS Code)](how-to-create-function-azure-cli?pivots=programming-language-javascript) or [Azure Functions Core Tools](how-to-create-function-vs-code?pivot=programming-language-javascript). This article uses "tip" alerts to highlight the most important concrete actions that you should take to upgrade your app.
Version 4 is designed to provide Node.js developers with the following benefits:

- Provide a familiar and intuitive experience to Node.js developers.
- Make the file structure flexible with support for full customization.
- Switch to a code-centric approach for defining function configuration.

## Considerations

- The Node.js programming model shouldn't be confused with the Azure Functions runtime:
**Programming model**: Defines how you author your code and is specific to JavaScript and TypeScript.**Runtime**: Defines underlying behavior of Azure Functions and is shared across all languages.

- The version of the programming model is strictly tied to the version of the
npm package. It's versioned independently of the`@azure/functions`

[runtime](functions-versions). Both the runtime and the programming model use the number 4 as their latest major version, but that's a coincidence. - You can't mix the v3 and v4 programming models in the same function app. As soon as you register one v4 function in your app, any v3 functions registered in
*function.json*files are ignored.

## Requirements

Version 4 of the Node.js programming model requires the following minimum versions:

npm package v4.0.0`@azure/functions`

[Node.js](https://nodejs.org/en/about/previous-releases)v18+[Azure Functions Runtime](functions-versions)v4.25+[Azure Functions Core Tools](functions-run-local)v4.0.5382+ (if running locally)

npm package v4.0.0`@azure/functions`

[Node.js](https://nodejs.org/en/about/previous-releases)v18+[TypeScript](https://www.typescriptlang.org/)v4+[Azure Functions Runtime](functions-versions)v4.25+[Azure Functions Core Tools](functions-run-local)v4.0.5382+ (if running locally)

## Include the npm package

In v4, the [ @azure/functions](https://www.npmjs.com/package/@azure/functions) npm package contains the primary source code that backs the Node.js programming model. In previous versions, that code shipped directly in Azure and the npm package had only the TypeScript types. You now need to include this package for both TypeScript and JavaScript apps. You

*can*include the package for existing v3 apps, but it isn't required.

Tip

Make sure the `@azure/functions`

package is listed in the `dependencies`

section (not `devDependencies`

) of your *package.json* file. You can install v4 by using the following command:

```
npm install @azure/functions
```


## Set your app entry point

In v4 of the programming model, you can structure your code however you want. The only files that you need at the root of your app are *host.json* and *package.json*.

Otherwise, you define the file structure by setting the `main`

field in your *package.json* file. You can set the `main`

field to a single file or multiple files by using a [glob pattern](https://wikipedia.org/wiki/Glob_(programming)). The following table shows example values for the `main`

field:

| Example | Description |
|---|---|
`src/index.js` |
Register functions from a single root file. |
`src/functions/*.js` |
Register each function from its own file. |
`src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

| Example | Description |
|---|---|
`dist/src/index.js` |
Register functions from a single root file. |
`dist/src/functions/*.js` |
Register each function from its own file. |
`dist/src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

Tip

Make sure you define a `main`

field in your *package.json* file.

## Switch the order of arguments

The trigger input, instead of the invocation context, is now the first argument to your function handler. The invocation context, now the second argument, is simplified in v4 and isn't as required as the trigger input. You can leave it off if you aren't using it.

Tip

Switch the order of your arguments. For example, if you're using an HTTP trigger, switch `(context, request)`

to either `(request, context)`

or just `(request)`

if you aren't using the context.

## Define your function in code

You no longer have to create and maintain those separate *function.json* configuration files. You can now fully define your functions directly in your TypeScript or JavaScript files. In addition, many properties now have defaults so that you don't have to specify them every time.

```
const { app } = require('@azure/functions');
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
},
});
```


```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: httpTrigger1,
});
```


Tip

Move the configuration from your *function.json* file to your code. The type of the trigger corresponds to a method on the `app`

object in the new model. For example, if you use an `httpTrigger`

type in *function.json*, call `app.http()`

in your code to register the function. If you use `timerTrigger`

, call `app.timer()`

.

## Review your usage of context

In v4, the `context`

object is simplified to reduce duplication and to make writing unit tests easier. For example, we streamlined the primary input and output so that they're accessed only as the argument and return value of your function handler.

You can't access the primary input and output on the `context`

object anymore, but you must still access *secondary* inputs and outputs on the `context`

object. For more information about secondary inputs and outputs, see the [Node.js developer guide](functions-reference-node#extra-inputs-and-outputs).

### Get the primary input as an argument

The primary input is also called the *trigger* and is the only required input or output. You must have one (and only one) trigger.

Version 4 supports only one way of getting the trigger input, as the first argument:

```
async function httpTrigger1(request, context) {
const onlyOption = request;
```


```
async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const onlyOption = request;
```


Tip

Make sure you aren't using `context.req`

or `context.bindings`

to get the input.

### Set the primary output as your return value

Version 4 supports only one way of setting the primary output, through the return value:

```
return {
body: `Hello, ${name}!`
};
```


```
async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
// ...
return {
body: `Hello, ${name}!`
};
}
```


Tip

Make sure you always return the output in your function handler, instead of setting it with the `context`

object.

### Context logging

In v4, logging methods were moved to the root `context`

object as shown in the following example. For more information about logging, see the [Node.js developer guide](functions-reference-node#logging).

```
context.log('This is an info log');
context.error('This is an error');
context.warn('This is an error');
```


### Create a test context

Version 3 doesn't support creating an invocation context outside the Azure Functions runtime, so authoring unit tests can be difficult. Version 4 allows you to create an instance of the invocation context, although the information during tests isn't detailed unless you add it yourself.

```
const testInvocationContext = new InvocationContext({
functionName: 'testFunctionName',
invocationId: 'testInvocationId'
});
```


## Review your usage of HTTP types

The HTTP request and response types are now a subset of the [fetch standard](https://developer.mozilla.org/docs/Web/API/fetch). They're no longer unique to Azure Functions.

The types use the [ undici](https://undici.nodejs.org/) package in Node.js. This package follows the fetch standard and is

[currently being integrated](https://github.com/nodejs/undici/issues/1737)into Node.js core.

### HttpRequest

*Body*. You can access the body by using a method specific to the type that you want to receive:`const body = await request.text(); const body = await request.json(); const body = await request.formData(); const body = await request.arrayBuffer(); const body = await request.blob();`

*Header*:`const header = request.headers.get('content-type');`

*Query parameter*:`const name = request.query.get('name');`


### HttpResponse

*Status*:`return { status: 200 };`

*Body*:Use the

`body`

property to return most types like a`string`

or`Buffer`

:`return { body: "Hello, world!" };`

Use the

`jsonBody`

property for the easiest way to return a JSON response:`return { jsonBody: { hello: "world" } };`

*Header*. You can set the header in two ways, depending on whether you're using the`HttpResponse`

class or the`HttpResponseInit`

interface:`const response = new HttpResponse(); response.headers.set('content-type', 'application/json'); return response;`

`return { headers: { 'content-type': 'application/json' } };`


Tip

Update any logic by using the HTTP request or response types to match the new methods.

Tip

Update any logic by using the HTTP request or response types to match the new methods. You should get TypeScript build errors to help you identify if you're using old methods.

## Troubleshoot

See the [Node.js Troubleshoot guide](functions-node-troubleshoot).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-twitter-email -->

# Tutorial: Create a function to integrate with Azure Logic Apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Azure Logic Apps in the Logic Apps Designer. This integration allows you use the computing power of Functions in orchestrations with other Azure and third-party services.

This tutorial shows you how to create a workflow to analyze X activity. As tweets are evaluated, the workflow sends notifications when positive sentiments are detected.

In this tutorial, you learn to:

- Create an Azure AI services API Resource.
- Create a function that categorizes tweet sentiment.
- Create a logic app that connects to X.
- Add sentiment detection to the logic app.
- Connect the logic app to the function.
- Send an email based on the response from the function.

## Prerequisites

- An active
[X](https://x.com/)account. - An
[Outlook.com](https://outlook.com/)account (for sending notifications).

Note

If you want to use the Gmail connector, only G-Suite business accounts can use this connector without restrictions in logic apps. If you have a Gmail consumer account, you can use the Gmail connector with only specific Google-approved apps and services, or you can [create a Google client app to use for authentication in your Gmail connector](/en-us/connectors/gmail/#authentication-and-bring-your-own-application).

For more information, see [Data security and privacy policies for Google connectors in Azure Logic Apps](../connectors/connectors-google-data-security-privacy-policy).

## Create Text Analytics resource

The Azure AI services APIs are available in Azure as individual resources. Use the Text Analytics API to detect the sentiment of posted tweets.

Sign in to the

[Azure portal](https://portal.azure.com/).Select

**Create a resource**in the upper left-hand corner of the Azure portal.Under

*Categories*, select**AI + Machine Learning**Under

*Text Analytics*, select**Create**.Enter the following values in the

*Create Text Analytics*screen.Setting Value Remarks Subscription Your Azure subscription name Resource group Create a new resource group named **tweet-sentiment-tutorial**Later, you delete this resource group to remove all the resources created during this tutorial. Region Select the region closest to you Name **TweetSentimentApp**Pricing tier Select **Free F0**Select

**Review + create**.Select

**Create**.Once the deployment is complete, select

**Go to Resource**.

## Get Text Analytics settings

With the Text Analytics resource created, you'll copy a few settings and set them aside for later use.

Select

**Keys and Endpoint**.Copy

**Key 1**by clicking on the icon at the end of the input box.Paste the value into a text editor.

Copy the

**Endpoint**by clicking on the icon at the end of the input box.Paste the value into a text editor.


## Create the function app

From the top search box, search for and select

**Function app**.Select

**Create**.Enter the following values.

Setting Suggested Value Remarks Subscription Your Azure subscription name Resource group **tweet-sentiment-tutorial**Use the same resource group name throughout this tutorial. Function App name **TweetSentimentAPI**+ a unique suffixFunction application names are globally unique. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.Publish **Code**Runtime stack **.NET**The function code provided for you is in C#. Version Select the latest version number Region Select the region closest to you Select

**Review + create**.Select

**Create**.Once the deployment is complete, select

**Go to Resource**.

## Create an HTTP-triggered function

From the left menu of the

*Functions*window, select**Functions**.Select

**Add**from the top menu and enter the following values.Setting Value Remarks Development environment **Develop in portal**Template **HTTP Trigger**New Function **TweetSentimentFunction**This is the name of your function. Authorization level **Function**Select the

**Add**button.Select the

**Code + Test**button.Paste the following code in the code editor window.

`#r "Newtonsoft.Json" using System; using System.Net; using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Logging; using Microsoft.Extensions.Primitives; using Newtonsoft.Json; public static async Task<IActionResult> Run(HttpRequest req, ILogger log) { string requestBody = String.Empty; using (StreamReader streamReader = new StreamReader(req.Body)) { requestBody = await streamReader.ReadToEndAsync(); } dynamic score = JsonConvert.DeserializeObject(requestBody); string value = "Positive"; if(score < .3) { value = "Negative"; } else if (score < .6) { value = "Neutral"; } return requestBody != null ? (ActionResult)new OkObjectResult(value) : new BadRequestObjectResult("Pass a sentiment score in the request body."); }`

A sentiment score is passed into the function, which returns a category name for the value.

Select the

**Save**button on the toolbar to save your changes.Note

To test the function, select

**Test/Run**from the top menu. On the*Input*tab, enter a value of`0.9`

in the*Body*input box, and then select**Run**. Verify that a value of*Positive*is returned in the*HTTP response content*box in the*Output*section.

Next, create a logic app that integrates with Azure Functions, X, and the Azure AI services API.

## Create a logic app

From the top search box, search for and select

**Logic Apps**.Select

**Add**.Select

**Consumption**and enter the following values.Setting Suggested Value Subscription Your Azure subscription name Resource group **tweet-sentiment-tutorial**Logic app name **TweetSentimentApp**Region Select the region closest to you, preferably the same region you selected in previous steps. Accept default values for all other settings.

Select

**Review + create**.Select

**Create**.Once the deployment is complete, select

**Go to Resource**.Select the

**Blank Logic App**button.Select the

**Save**button on the toolbar to save your progress.

You can now use the Logic Apps Designer to add services and triggers to your application.

## Connect to X

Create a connection to X so your app can poll for new tweets.

Search for

**X**in the top search box.Select the

**X**icon.Select the

**When a new tweet is posted**trigger.Enter the following values to set up the connection.

Setting Value Connection name **MyXConnection**Authentication Type **Use default shared application**Select

**Sign in**.Follow the prompts in the pop-up window to complete signing in to X.

Next, enter the following values in the

*When a new tweet is posted*box.Setting Value Search text **#my-x-tutorial**How often do you want to check for items? **1**in the textbox, and

**Hour**in the dropdown. You may enter different values but be sure to review the current[limitations](/en-us/connectors/twitterconnector/#limits)of the X connector.Select the

**Save**button on the toolbar to save your progress.

Next, connect to text analytics to detect the sentiment of collected tweets.

## Add Text Analytics sentiment detection

Select

**New step**.Search for

**Text Analytics**in the search box.Select the

**Text Analytics**icon.Select

**Detect Sentiment**and enter the following values.Setting Value Connection name **TextAnalyticsConnection**Account Key Paste in the Text Analytics account key you set aside earlier. Site URL Paste in the Text Analytics endpoint you set aside earlier. Select

**Create**.Click inside the

*Add new parameter*box, and check the box next to**documents**that appears in the pop-up.Click inside the

*documents Id - 1*textbox to open the dynamic content pop-up.In the

*dynamic content*search box, search for**id**, and click on**Tweet id**.Click inside the

*documents Text - 1*textbox to open the dynamic content pop-up.In the

*dynamic content*search box, search for**text**, and click on**Tweet text**.In

**Choose an action**, type**Text Analytics**, and then click the**Detect sentiment**action.Select the

**Save**button on the toolbar to save your progress.

The *Detect Sentiment* box should look like the following screenshot.


## Connect sentiment output to function endpoint

Select

**New step**.Search for

**Azure Functions**in the search box.Select the

**Azure Functions**icon.Search for your function name in the search box. If you followed the guidance above, your function name begins with

**TweetSentimentAPI**.Select the function icon.

Select the

**TweetSentimentFunction**item.Click inside the

*Request Body*box, and select the*Detect Sentiment***score**item from the pop-up window.Select the

**Save**button on the toolbar to save your progress.

## Add conditional step

Select the

**Add an action**button.Click inside the

*Control*box, and search for and select**Control**in the pop-up window.Select

**Condition**.Click inside the

*Choose a value*box, and select the*TweetSentimentFunction***Body**item from the pop-up window.Enter

**Positive**in the*Choose a value*box.Select the

**Save**button on the toolbar to save your progress.

## Add email notifications

Under the

*True*box, select the**Add an action**button.Search for and select

**Office 365 Outlook**in the text box.Search for

**send**and select**Send an email**in the text box.Select the

**Sign in**button.Follow the prompts in the pop-up window to complete signing in to Office 365 Outlook.

Enter your email address in the

*To*box.Click inside the

*Subject*box and click on the**Body**item under*TweetSentimentFunction*. If the*Body*item isn't shown in the list, click the**See more**link to expand the options list.After the

*Body*item in the*Subject*, enter the text**Tweet from:**.After the

*Tweet from:*text, click on the box again and select**User name**from the*When a new tweet is posted*options list.Click inside the

*Body*box and select**Tweet text**under the*When a new tweet is posted*options list. If the*Tweet text*item isn't shown in the list, click the**See more**link to expand the options list.Select the

**Save**button on the toolbar to save your progress.

The email box should now look like this screenshot.


## Run the workflow

From your X account, tweet the following text:

**I'm enjoying #my-x-tutorial**.Return to the Logic Apps Designer and select the

**Run**button.Check your email for a message from the workflow.


## Clean up resources

To clean up all the Azure services and accounts created during this tutorial, delete the resource group.

Search for

**Resource groups**in the top search box.Select the

**tweet-sentiment-tutorial**.Select

**Delete resource group**Enter

**tweet-sentiment-tutorial**in the text box.Select the

**Delete**button.

Optionally, you may want to return to your X account and delete any test tweets from your feed.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache -->

# Overview of Azure functions for Azure Redis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use either Azure Managed Redis or Azure Cache for Redis with Azure Functions to create optimized serverless and event-driven architectures.

Azure Functions provides an event-driven programming model where triggers and bindings are key features. With Azure Functions, you can easily build event-driven serverless applications. Azure Redis services (Azure Managed Redis and Azure Cache for Redis) provide a set of building blocks and best practices for building distributed applications, including microservices, state management, pub/sub messaging, and more.

Azure Redis can be used as a trigger for Azure Functions, allowing you to initiate a serverless workflow. This functionality can be highly useful in data architectures like a write-behind cache, or any event-based architectures.

You can integrate Azure Redis and Azure Functions to build functions that react to events from Azure Redis or external systems.

| Action | Direction |
|---|---|
|

[Trigger on Redis lists](functions-bindings-cache-trigger-redislist)[Trigger on Redis streams](functions-bindings-cache-trigger-redisstream)[Read a cached value](functions-bindings-cache-input)[Write a values to cache](functions-bindings-cache-output)## Scope of availability for functions triggers and bindings

| Tier | Azure Cache for Redis (Basic, Standard, Premium, Enterprise, Enterprise Flash) | Azure Managed Redis (Memory Optimized, Basic, Compute Optimized, Flash Optimized) |
|---|---|---|
| Pub/Sub | Yes | Yes |
| Lists | Yes | Yes |
| Streams | Yes | Yes |
| Bindings | Yes | Yes |

Important

Redis triggers are currently only supported for functions running in either a [Elastic Premium plan](functions-premium-plan) or a dedicated [App Service plan](dedicated-plan).

## Install extension

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Redis).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Redis
```


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

## Update packages

Add the [Azure Functions Java Redis Annotations package](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-redis) to your project by updating the `pom.xml`

file to add this dependency:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-redis</artifactId>
<version>1.0.0</version>
</dependency>
```


## Redis connection string

Azure Redis triggers and bindings have a required property that indicates the application setting or collection name that contains cache connection information. The Redis trigger or binding looks for an environmental variable holding the connection string with the name passed to the `Connection`

parameter.

In local development, the `Connection`

can be defined using the [local.settings.json](/en-us/azure/azure-functions/functions-develop-local#local-settings-file) file. When deployed to Azure, [application settings](/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings) can be used.

When connecting to a cache instance with an Azure function, you can use one of these kinds of connections in your deployments:

A user-assigned managed identity must be associated with your function app, and that identity must also be granted explicit permissions in your cache service. For more information, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

These examples show the key name and value of app settings required to connect to each cache service based on the kind of client authentication, assuming that the `Connection`

property in the binding is set to `Redis`

.

```
"Redis__redisHostName": "<cacheName>.<region>.redis.azure.net",
"Redis__principalId": "<principalId>",
"Redis__clientId": "<clientId>"
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/disable-function -->

# How to disable functions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to disable a function in Azure Functions. To *disable* a function means to make the runtime ignore the event intended to trigger the function. This ability lets you prevent a specific function from running without having to modify and republish the entire function app.

You can disable a function in place by creating an app setting in the format `AzureWebJobs.<FUNCTION_NAME>.Disabled`

set to `true`

. You can create and modify this application setting in several ways, including by using the [Azure CLI](/en-us/cli/azure/), [Azure PowerShell](/en-us/powershell/azure/), and from your function's **Overview** tab in the [Azure portal](https://portal.azure.com).

Note

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the [Flex Consumption plan](flex-consumption-plan) with [rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments) for guidance on minimizing downtime.

## Disable a function

Use one of these modes to create an app setting that disables an example function named `QueueTrigger`

:

Use the **Enable** and **Disable** buttons on the function's **Overview** page. These buttons work by changing the value of the `AzureWebJobs.QueueTrigger.Disabled`

app setting. The function-specific app setting is created the first time a function is disabled.

Even when you publish to your function app from a local project, you can still use the portal to disable functions in the function app.

Note

Disabled functions can still be run by calling the REST endpoint using a master key. To learn more, see [Run a disabled function](#run-a-disabled-function). This means that a disabled function still runs when started from the **Test/Run** window in the portal using the **master (Host key)**.

## Disable functions in a slot

By default, app settings also apply to apps running in deployment slots. You can, however, override the app setting used by the slot by setting a slot-specific app setting. For example, you might want a function to be active in production but not during deployment testing. It's common to disable timer triggered functions in slots to prevent simultaneous executions.

To disable a function only in the staging slot:

Navigate to the slot instance of your function app by selecting **Deployment slots** under **Deployment**, choosing your slot, and selecting **Functions** in the slot instance. Choose your function, then use the **Enable** and **Disable** buttons on the function's **Overview** page. These buttons work by changing the value of the `AzureWebJobs.<FUNCTION_NAME>.Disabled`

app setting. This function-specific setting is created the first time you disable the function.

You can also directly add the app setting named `AzureWebJobs.<FUNCTION_NAME>.Disabled`

with value of `true`

in the **Configuration** for the slot instance. When you add a slot-specific app setting, make sure to check the **Deployment slot setting** box. This option maintains the setting value with the slot during swaps.

To learn more, see [Azure Functions Deployment slots](functions-deployment-slots).

## Run a disabled function

You can still cause a disabled function to run by supplying the master access key (`_master`

) in a REST request to the endpoint URL of the disabled function. In this way, you can develop and validate functions in Azure in a disabled state while preventing them from being accessed by others. Using any other type of key in the request returns an HTTP 404 response.

Caution

Due to the elevated permissions in your function app granted by the master key, you shouldn't share this key with third parties or distribute it in native client applications. Use caution when choosing the admin HTTP access level for your function endpoints.

To learn more about the master key, see [Understand keys](function-keys-how-to#understand-keys). To learn more about calling non-HTTP triggered functions, see [Manually run a non HTTP-triggered function](functions-manually-run-non-http).

## Disable functions locally

Functions can be disabled in the same way when running locally. To disable a function named `QueueTrigger`

, add an entry to the Values collection in the local.settings.json file, as follows:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "python",
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"AzureWebJobs.QueueTrigger.Disabled": true
}
}
```


## Considerations

Keep the following considerations in mind when you disable functions:

When you disable an HTTP triggered function by using the methods described in this article, the endpoint can still be accessed when running on your local computer and

[in the portal](#run-a-disabled-function).At this time, function names that contain a hyphen (

`-`

) can't be disabled when running on Linux. If you plan to disable your functions when running on Linux, don't use hyphens in your function names.

## Next steps

This article is about disabling automatic triggers. For more information about triggers, see [Triggers and bindings](functions-triggers-bindings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/extension-bundles -->

# Azure Functions extension bundles

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how extension bundles enable your function code to use all of the [triggers and bindings that Azure Functions supports](functions-triggers-bindings). You also learn about the support levels and policies for your apps when you use extension bundles.

This article applies only to Azure Functions developers who use non-.NET languages. To learn how to add binding extensions directly to your C# function apps, see [Register Azure Functions binding extensions](functions-bindings-register).

## Overview

Extension bundles add a predefined set of compatible binding extensions to your function app. A bundle contains all of the binding extensions currently supported by Functions. Extension bundles are versioned. Each version contains a specific set of binding extension versions that are verified to work together.

You should always use the latest bundle version in your app, when possible.

When you create an Azure Functions project from a non-.NET template, extension bundles are already enabled in the app's `host.json`

file.

## Define an extension bundle reference

You define an extension bundle reference in the `host.json`

project file by adding an `extensionBundle`

section, as in this example:

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

## Bundle versions

This table lists all `Microsoft.Azure.Functions.ExtensionBundle`

versions and the current [support state](#extension-bundles-support-policy):

| Bundle version | Version in host.json | Support state* |
|---|---|---|
|

`[4.0.0, 5.0.0)`

`[4.*, 5.0.0)`

[3.x](https://github.com/Azure/azure-functions-extension-bundles/blob/main-v3/src/Microsoft.Azure.Functions.ExtensionBundle/extensions.json)`[3.3.0, 4.0.0)`

[2.x](https://github.com/Azure/azure-functions-extension-bundles/blob/main-v2/src/Microsoft.Azure.Functions.ExtensionBundle/extensions.json)`[2.*, 3.0.0)`

[1.x](https://github.com/Azure/azure-functions-extension-bundles/blob/v1.x/src/Microsoft.Azure.Functions.ExtensionBundle/extensions.json)`[1.*, 2.0.0)`

* Deprecated bundle versions can include deprecated binding extension versions. For optimal supportability and reliability, you should [upgrade to bundle version 4.x](#upgrade-extension-bundles).

By default, extension bundles are defined via version ranges, which guarantees that the latest minor bundle version is used. Select a version link in the table to review the `extensions.json`

file that defines the latest bundle for that major version.

## Considerations for extension bundles

Keep these considerations in mind when you work with extension bundles:

- When possible, you should set a
`version`

range value in`host.json`

from the preceding table, such as`[4.0.0, 5.0.0)`

, instead of defining a custom range. - Use the latest version range to obtain optimal app performance and access to the latest features.
- In the unlikely event that you can't use an extension bundle, you must instead
[explicitly install extensions](functions-bindings-register#explicitly-install-extensions). - When updating the extensions used by a deployed app, Functions downloads new extension versions from the
`cdn.functions.azure.com`

endpoint. For extension updates to succeed, the`cdn.functions.azure.com`

endpoint must be accessible to your function app.

## Upgrade extension bundles

It's important to keep your bundle version up-to-date so that your apps can continue to be eligible for new features, security patches, and performance optimizations.

To upgrade your app to the most recent bundle, edit the host.json file in the root of your app project. Set the value of `extensionBundle.version`

to `[4.0.0,5.0.0)`

, which should look like this in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


Keep these considerations in mind when upgrading the extension bundle version used by your app:

- The contents of the latest 4.x bundle can always be found at
[this release page in the repo](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). - Review the reference documentation for any extensions used by your app to look for any breaking changes between versions. For the list of extension versions included in the default bundle, see the
`extension.json`

project file linked[from this table](#bundle-versions). You can review the[bundle releases page](https://github.com/Azure/azure-functions-extension-bundles/releases)in the bundles repo for specific bundle version tags. - Always verify your app locally after upgrading the bundle version to ensure compatibility with the updated extensions. You can use the
[func start](functions-core-tools-reference#func-start)command in Azure Functions Core Tools or F5 in Visual Studio or Visual Studio Code to run your function app locally. - The way that you trigger extensions to be updated based on changes to the bundle version in the host.json file depends on your app environment:
- Local project: extensions are updated locally when Core Tools starts, either from the
`func start`

command or when debugging in your development tools. - Function app: extensions are updated when you deploy the updated host.json file to your function app in Azure.

- Local project: extensions are updated locally when Core Tools starts, either from the

## Extension bundles support policy

Major version releases of an extension bundle can occur when there are breaking change updates in one of the contained binding extensions. These extension breaking changes require updates to the bundle to remain compatible with the underlying Azure SDKs. Upgrading the bundle ensures your apps continue to receive new features, performance improvements, and full product support.

Note

Because extension bundle updates are driven by updates in the underlying Azure SDKs, the support cycle for extension bundles generally follows the [support policies of the underlying Azure SDKs](https://azure.github.io/azure-sdk/policies_support.html).

Microsoft notifies you when an extension bundle or a binding extension version is deprecated. These notifications might appear in different parts of your Functions experience, such as in host logs, Application Insights tables, or the Azure portal. When you encounter these notifications, you must start the process of planning for and upgrading your function apps to the latest supported extension bundle version.

The support cycle of extension bundles follows these distinct phases:

| Phase | Description |
|---|---|
Preview |
Prerelease versions of specific binding extensions are maintained in a preview extension bundle (`Microsoft.Azure.Functions.ExtensionBundle.Preview` ). You can use this preview extension bundle to take advantage of preview extensions and new behaviors in existing extensions before they reach general availability (GA). For more information, see
|
Active |
The most recent major version of extension bundles is considered to be the active version. We recommend this version for your function apps. |
Deprecation |
The bundle version is superseded by a more recent release and is now deprecated. After a bundle is deprecated, it only receives critical bug fixes and security updates for a limited overlap period. This overlap is typically at least 12 months, which gives you time to plan, test, and upgrade your apps to the latest bundle version. Function apps that continue to use a deprecated bundle can still run on the platform. However, to ensure access to new features, performance improvements, security patches, and full support, you must upgrade your function apps to a supported bundle version. |

You can view the extension bundle versions and their included extensions in the [Azure Functions extension bundles repository](https://github.com/Azure/azure-functions-extension-bundles/releases). You can also view the Azure SDK releases page for an inventory of all Functions extensions. You can find individual .NET packages on [NuGet.org](https://nuget.org/).

## Work with preview extension bundles

Keep these considerations in mind when you choose to use a non-GA extension bundle:

- Preview bundles can include features that are still under development and not yet ready for production use. They're intended for evaluation and testing in nonproduction environments.
- Breaking changes occur between preview versions without prior notice. They can include changes to:
- Trigger and binding definitions.
- Extensions included in the preview.
- Performance characteristics and stability.

- Security updates might require you to upgrade versions.
- You must completely test preview bundles in nonproduction environments and avoid using preview bundles in production. When you must use a preview bundle in production, take these extra precautions:
- Pin your bundle to a specific, well-tested bundle version instead of to a range. Pinning prevents automatic upgrading of your bundle version before you have a chance to verify the update in a nonproduction environment.
- Move your app to using a GA bundle version as soon as the functionality becomes available in a fully supported bundle release.

- To stay informed about bundle updates, including moving from preview to GA, you should:
- Monitor releases of preview bundle versions on the
[release page for extension bundles](https://github.com/Azure/azure-functions-extension-bundles/releases). - Monitor
[extension-specific reference documentation](functions-triggers-bindings). - Review the NuGet package versions of specific preview extensions that you're using.
- Track significant updates or changes in the change logs published on NuGet.org for each preview extension.

- Monitor releases of preview bundle versions on the

## Related content

- To learn more about binding extensions, see
[Register Azure Functions binding extensions](functions-bindings-register).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-opentelemetry-distributed-tracing -->

# Tutorial: Monitor Azure Functions with OpenTelemetry distributed tracing

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates OpenTelemetry support in Azure Function, which enables distributed tracing across multiple function calls by using integrated Application Insights and OpenTelemetry support. To help you get started, an Azure Developer CLI (`azd`

) template is used to create your code project as well as the Azure deployment in which to run your app.

In this tutorial, you use the `azd`

tool to:

- Initialize an OpenTelemetry-enabled project from a template.
- Review the code that enables OpenTelemetry integration.
- Run and verify your OpenTelemetry-enabled app locally.
- Create a function app and related resources in Azure.
- Deploy your code project to the function app in Azure.
- Verify distributed tracing in Application Insights.

The required Azure resources created by this template follow current best practices for secure and scalable function app deployments in Azure. The same `azd`

command also deploys your code project to your new function app in Azure.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Important

This article currently supports only C#, Python, and TypeScript. To complete the quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template that includes OpenTelemetry distributed tracing.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

## Review the code

The template creates a complete distributed tracing scenario with three functions that work together. Let's review the key OpenTelemetry-related aspects:

### OpenTelemetry configuration

The `src/otel-sample/host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"extensions": {
"serviceBus": {
"maxConcurrentCalls": 10
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


The key setting `"telemetryMode": "OpenTelemetry"`

enables distributed tracing across function calls.

The `src/OTelSample/host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"OpenTelemetry": {
"logLevel": {
"Host.General": "Warning"
}
}
}
}
```


The key setting `"telemetryMode": "OpenTelemetry"`

enables distributed tracing across function calls.

### Dependencies for OpenTelemetry

The `src/otel-sample/requirements.txt`

file includes the necessary packages for OpenTelemetry integration:

```
azure-functions
azure-monitor-opentelemetry
requests
```


The `azure-monitor-opentelemetry`

package provides the OpenTelemetry integration with Application Insights.

The `src/otel-sample/package.json`

file includes the necessary packages for OpenTelemetry integration:

```
{
"dependencies": {
"@azure/functions": "^4.0.0",
"@azure/functions-opentelemetry-instrumentation": "^0.1.0",
"@azure/monitor-opentelemetry-exporter": "^1.0.0",
"axios": "^1.6.0"
}
}
```


The `@azure/functions-opentelemetry-instrumentation`

and `@azure/monitor-opentelemetry-exporter`

packages provide the OpenTelemetry integration with Application Insights.

The `.csproj`

file includes the necessary packages for OpenTelemetry integration:

```
<PackageReference Include="Azure.Monitor.OpenTelemetry.Exporter" Version="1.4.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.OpenTelemetry" Version="1.4.0" />
<PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.10.0" />
```


These packages provide the OpenTelemetry integration with Application Insights and HTTP instrumentation for distributed tracing.

### Function implementation

The functions in `src/otel-sample/function_app.py`

demonstrate a distributed tracing flow:

#### First HTTP Function

```
@app.function_name("first_http_function")
@app.route(route="first_http_function", auth_level=func.AuthLevel.ANONYMOUS)
def first_http_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Python HTTP trigger function (first) processed a request.')
# Call the second function
base_url = f"{req.url.split('/api/')[0]}/api"
second_function_url = f"{base_url}/second_http_function"
response = requests.get(second_function_url)
second_function_result = response.text
result = {
"message": "Hello from the first function!",
"second_function_response": second_function_result
}
return func.HttpResponse(
json.dumps(result),
status_code=200,
mimetype="application/json"
)
```


#### Second HTTP Function

```
@app.function_name("second_http_function")
@app.route(route="second_http_function", auth_level=func.AuthLevel.ANONYMOUS)
@app.service_bus_queue_output(arg_name="outputsbmsg", queue_name="%ServiceBusQueueName%",
connection="ServiceBusConnection")
def second_http_function(req: func.HttpRequest, outputsbmsg: func.Out[str]) -> func.HttpResponse:
logging.info('Python HTTP trigger function (second) processed a request.')
message = "This is the second function responding."
# Send a message to the Service Bus queue
queue_message = "Message from second HTTP function to trigger ServiceBus queue processing"
outputsbmsg.set(queue_message)
logging.info('Sent message to ServiceBus queue: %s', queue_message)
return func.HttpResponse(
message,
status_code=200
)
```


#### Service Bus Queue Trigger

```
@app.service_bus_queue_trigger(arg_name="azservicebus", queue_name="%ServiceBusQueueName%",
connection="ServiceBusConnection")
def servicebus_queue_trigger(azservicebus: func.ServiceBusMessage):
logging.info('Python ServiceBus Queue trigger start processing a message: %s',
azservicebus.get_body().decode('utf-8'))
time.sleep(5) # Simulate processing work
logging.info('Python ServiceBus Queue trigger end processing a message')
```


The OpenTelemetry configuration is set up in `src/otel-sample/index.ts`

:

```
import { AzureFunctionsInstrumentation } from '@azure/functions-opentelemetry-instrumentation';
import { AzureMonitorTraceExporter, AzureMonitorLogExporter } from '@azure/monitor-opentelemetry-exporter';
import { getNodeAutoInstrumentations, getResourceDetectors } from '@opentelemetry/auto-instrumentations-node';
import { registerInstrumentations } from '@opentelemetry/instrumentation';
import { detectResources } from '@opentelemetry/resources';
import { LoggerProvider, SimpleLogRecordProcessor } from '@opentelemetry/sdk-logs';
import { NodeTracerProvider, SimpleSpanProcessor } from '@opentelemetry/sdk-trace-node';
const resource = detectResources({ detectors: getResourceDetectors() });
const tracerProvider = new NodeTracerProvider({
resource,
spanProcessors: [new SimpleSpanProcessor(new AzureMonitorTraceExporter())]
});
tracerProvider.register();
const loggerProvider = new LoggerProvider({
resource,
processors: [new SimpleLogRecordProcessor(new AzureMonitorLogExporter())],
});
registerInstrumentations({
tracerProvider,
loggerProvider,
instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()],
});
```


The functions are defined in the `src/otel-sample/src/functions`

folder:

#### First HTTP Function

```
export async function firstHttpFunction(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log("TypeScript HTTP trigger function (first) processed a request.");
try {
// Call the second function
const baseUrl = request.url.split("/api/")[0];
const secondFunctionUrl = `${baseUrl}/api/second_http_function`;
const response = await axios.get(secondFunctionUrl);
const secondFunctionResult = response.data;
const result = {
message: "Hello from the first function!",
second_function_response: secondFunctionResult,
};
return {
status: 200,
body: JSON.stringify(result),
headers: { "Content-Type": "application/json" },
};
} catch (error) {
return {
status: 500,
body: JSON.stringify({ error: "Failed to process request" }),
};
}
}
```


#### Second HTTP Function

```
export async function secondHttpFunction(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log("TypeScript HTTP trigger function (second) processed a request.");
const message = "This is the second function responding.";
// Send a message to the Service Bus queue
const queueMessage =
"Message from second HTTP function to trigger ServiceBus queue processing";
context.extraOutputs.set(serviceBusOutput, queueMessage);
context.log("Sent message to ServiceBus queue:", queueMessage);
return {
status: 200,
body: message,
};
}
```


#### Service Bus Queue Trigger

```
export async function serviceBusQueueTrigger(
message: unknown,
context: InvocationContext
): Promise<void> {
context.log("TypeScript ServiceBus Queue trigger start processing a message:", message);
// Simulate processing time
await new Promise((resolve) => setTimeout(resolve, 5000));
context.log("TypeScript ServiceBus Queue trigger end processing a message");
}
```


The OpenTelemetry configuration is set up in `src/OTelSample/Program.cs`

:

```
using Azure.Monitor.OpenTelemetry.Exporter;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.OpenTelemetry;
using OpenTelemetry.Trace;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Logging.AddOpenTelemetry(logging =>
{
logging.IncludeFormattedMessage = true;
logging.IncludeScopes = true;
});
builder.Services.AddOpenTelemetry()
.WithTracing(tracing =>
{
tracing.AddHttpClientInstrumentation();
});
builder.Services.AddOpenTelemetry().UseAzureMonitorExporter();
builder.Services.AddOpenTelemetry().UseFunctionsWorkerDefaults();
builder.Services.AddHttpClient();
builder.Build().Run();
```


The functions are defined in separate class files:

#### First HTTP Function

```
public class FirstHttpTrigger
{
private readonly ILogger<FirstHttpTrigger> _logger;
private readonly IHttpClientFactory _httpClientFactory;
public FirstHttpTrigger(ILogger<FirstHttpTrigger> logger, IHttpClientFactory httpClientFactory)
{
_logger = logger;
_httpClientFactory = httpClientFactory;
}
[Function("first_http_function")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
{
_logger.LogInformation("first_http_function function processed a request.");
var baseUrl = $"{req.Url.AbsoluteUri.Split("/api/")[0]}/api";
var targetUri = $"{baseUrl}/second_http_function";
var client = _httpClientFactory.CreateClient();
var response = await client.GetAsync(targetUri);
var content = await response.Content.ReadAsStringAsync();
return new OkObjectResult($"Called second_http_function, status: {response.StatusCode}, content: {content}");
}
}
```


#### Second HTTP Function

```
public class SecondHttpTrigger
{
private readonly ILogger<SecondHttpTrigger> _logger;
public SecondHttpTrigger(ILogger<SecondHttpTrigger> logger)
{
_logger = logger;
}
[Function("second_http_function")]
public MultiResponse Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
{
_logger.LogInformation("second_http_function function processed a request.");
return new MultiResponse
{
Messages = new string[] { "Hello" },
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.OK)
};
}
}
public class MultiResponse
{
[ServiceBusOutput("%ServiceBusQueueName%", Connection = "ServiceBusConnection")]
public string[]? Messages { get; set; }
[HttpResult]
public HttpResponseData? HttpResponse { get; set; }
}
```


#### Service Bus Queue Trigger

```
public class ServiceBusQueueTrigger
{
private readonly ILogger<ServiceBusQueueTrigger> _logger;
public ServiceBusQueueTrigger(ILogger<ServiceBusQueueTrigger> logger)
{
_logger = logger;
}
[Function("servicebus_queue_trigger")]
public async Task Run(
[ServiceBusTrigger("%ServiceBusQueueName%", Connection = "ServiceBusConnection")]
ServiceBusReceivedMessage message,
ServiceBusMessageActions messageActions)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
// Complete the message
await messageActions.CompleteMessageAsync(message);
}
}
```


### Distributed tracing flow

This architecture creates a complete distributed tracing scenario, with this behavior:

**First HTTP function**receives an HTTP request and calls the second HTTP function**Second HTTP function**responds and sends a message to Service Bus**Service Bus trigger**processes the message with a delay to simulate processing work

Key aspects of the OpenTelemetry implementation:

**OpenTelemetry integration**: The`host.json`

file enables OpenTelemetry with`"telemetryMode": "OpenTelemetry"`

**Function chaining**: The first function calls the second using HTTP requests, creating correlated traces**Service Bus integration**: The second function outputs to Service Bus, which triggers the third function**Anonymous authentication**: The HTTP functions use`auth_level=func.AuthLevel.ANONYMOUS`

, so no function keys are required

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-azd-otel).

**OpenTelemetry integration**: The`index.ts`

file configures OpenTelemetry with Azure Monitor exporters for traces and logs**Function chaining**: The first function calls the second using axios with automatic trace propagation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**Processing simulation**: The 5-second delay in the Service Bus trigger simulates message processing work

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-otel).

**OpenTelemetry integration**: The`Program.cs`

file configures OpenTelemetry with Azure Monitor exporter**Function chaining**: The first function calls the second using HttpClient with OpenTelemetry instrumentation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**.NET 8 Isolated Worker**: Uses the latest Azure Functions .NET Isolated Worker model for better performance and flexibility

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel).

After you verify your functions locally, it's time to publish them to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure with OpenTelemetry support.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices, including managed identity connections.

Run this command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. The

`azd up`

command uses your response to these prompts with the Bicep configuration files to complete these deployment tasks:Create and configure these required Azure resources (equivalent to

`azd provision`

):- Azure Functions Flex Consumption plan and function app with OpenTelemetry enabled
- Azure Storage (required) and Application Insights (recommended)
- Service Bus namespace and queue for distributed tracing demonstration
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Test distributed tracing

Now you can test the OpenTelemetry distributed tracing functionality by calling your deployed functions and observing the telemetry in Application Insights.

### Invoke the function on Azure

You can invoke your function endpoints in Azure by making HTTP requests to their URLs. Since the HTTP functions in this template are configured with anonymous access, no function keys are required.

In your local terminal or command prompt, run this command to get the function app name and construct the URL:

`APP_NAME=$(azd env get-value AZURE_FUNCTION_NAME) echo "Function URL: https://$APP_NAME.azurewebsites.net/api/first_http_function"`

The

`azd env get-value`

command gets your function app name from the local environment.Test the function in your browser by navigating to the URL:

`https://your-function-app.azurewebsites.net/api/first_http_function`

Replace

`your-function-app`

with your actual function app name from the previous step. This single request creates a distributed trace that flows through all three functions.

### View distributed tracing in Application Insights

After invoking the function, you can observe the complete distributed trace in Application Insights:

Note

It might take a few minutes for telemetry data to appear in Application Insights after invoking your function. If you don't see data immediately, wait a few minutes and refresh the view.

Go to your Application Insights resource in the Azure portal (you can find it in the same resource group as your function app).

Open the

**Application map**to see the distributed trace across all three functions. You should see the flow from the HTTP request through your functions and to Service Bus.Check the

**Transaction search**to find your request and see the complete trace timeline. Search for transactions from your function app.Select a specific transaction to see the end-to-end trace that shows:

- The HTTP request to
`first_http_function`

- The internal HTTP call to
`second_http_function`

- The Service Bus message being sent
- The
`servicebus_queue_trigger`

processing the message from Service Bus

- The HTTP request to
In the trace details, you can see:

**Timing information**: How long each step took**Dependencies**: The connections between functions**Logs**: Application logs correlated with the trace**Performance metrics**: Response times and throughput


This example demonstrates end-to-end distributed tracing across multiple Azure Functions with OpenTelemetry integration, providing complete visibility into your application's behavior and performance.

## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

The latest deployment package always overwrites deployed code files.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that the command uses when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code -->

# Develop Azure Functions by using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Azure Functions extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions) lets you develop functions locally and deploy them to Azure. If this experience is your first with Azure Functions, you can learn more at [An introduction to Azure Functions](functions-overview).

The Azure Functions extension provides these benefits:

- Edit, build, and run functions on your local development computer.
- Publish your Azure Functions project directly to Azure.
- Write your functions in various languages while taking advantage of the benefits of Visual Studio Code.

You're viewing the C# version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp).

You're viewing the Java version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-java).

You're viewing the JavaScript version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-javascript).

You're viewing the PowerShell version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-powershell).

You're viewing the Python version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-python).

You're viewing the TypeScript version of this article. Make sure to select your preferred Functions programming language at the start of the article.


If you're new to Functions, you might want to first complete the [Visual Studio Code quickstart article](how-to-create-function-vs-code?pivot=programming-language-typescript).

Important

Don't mix local development and portal development for a single function app. When you publish from a local project to a function app, the deployment process overwrites any functions that you developed in the portal.

## Prerequisites

[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). You can also install the[Azure Tools extension pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack), which is recommended for working with Azure resources.An active

[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing). If you don't yet have an account, you can create one from the extension in Visual Studio Code.

You also need these prerequisites to [run and debug your functions locally](#run-functions-locally). They're not required to just create or publish projects to Azure Functions.

- The
[Azure Functions Core Tools](functions-run-local), which enables an integrated local debugging experience. When you have the Azure Functions extension installed, the easiest way to install or update Core Tools is by running the`Azure Functions: Install or Update Azure Functions Core Tools`

command from the command palette.

The

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.[.NET (CLI)](/en-us/dotnet/core/tools/), which is included in the .NET SDK.

[Java](/en-us/azure/developer/java/fundamentals/java-support-on-azure), one of the[supported versions](functions-reference-java#java-versions).

[Node.js](https://nodejs.org/), one of the[supported versions](functions-reference-node#node-version). Use the`node --version`

command to check your version.

[PowerShell 7.2](/en-us/powershell/scripting/install/installing-powershell-core-on-windows)recommended. For version information, see[PowerShell versions](functions-reference-powershell#powershell-versions).

[Python](https://www.python.org/downloads/), one of the[supported versions](functions-reference-python#supported-python-versions).[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Create an Azure Functions project

The Functions extension lets you create the required function app project at the same time you create your first function. Use these steps to create an HTTP-triggered function in a new project. An [HTTP trigger](functions-bindings-http-webhook) is the simplest function trigger template to demonstrate.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

. Select the directory location for your project workspace, then choose**Select**.You can either create a new folder or choose an empty folder for the project workspace, but don't choose a project folder that's already part of a workspace.

You can instead run the command

`Azure Functions: Create New Containerized Project...`

to also get a Dockerfile generated for the project.When prompted,

**Select a language**for your project. If necessary, choose a specific language version.Select the

**HTTP trigger**function template, or select**Skip for now**to create a project without a function. You can always[add a function to your project](#add-a-function-to-your-project)later.Tip

To view additional templates, select the

**Change template filter**option and set the value to**Core**or**All**.For the function name, enter

**HttpExample**, select Enter, then select**Function**authorization.This authorization level requires that you provide a

[function key](function-keys-how-to)when you call the function endpoint.From the dropdown list, select

**Add to workspace**.In the

**Do you trust the authors of the files in this folder?**window, select**Yes**.

Visual Studio Code creates a function in your chosen language and in the template for an HTTP-triggered function.

### Generated project files

The project template creates a project in your chosen language and installs the required dependencies. For any language, the new project has these files:

**host.json**: Lets you configure the Functions host. These settings apply when you're running functions locally and when you're running them in Azure. For more information, see[host.json reference](functions-host-json).**local.settings.json**: Maintains settings used when you're locally running functions. These settings are used only when you're running functions locally. For more information, see[Local settings file](#local-settings).Important

Because the

**local.settings.json**file can contain secrets, make sure to exclude the file from your project source control.**Dockerfile**(optional): Lets you create a containerized function app from your project by using an approved base image for your project. You only get this file when you run the command`Azure Functions: Create New Containerized Project...`

. You can add a Dockerfile to an existing project by using the`func init --docker-only`

command in[Core Tools](functions-core-tools-reference#func-init).

An HttpExample.cs class library file, the contents of which vary depending on whether your project runs in an [isolated worker process](dotnet-isolated-process-guide#project-structure) or [in-process](functions-dotnet-class-library#functions-class-library-project) with the Functions host.

These files are created:

A pom.xml file in the root folder that defines the project and deployment parameters, including project dependencies and the

[Java version](functions-reference-java#java-versions). The pom.xml also contains information about the Azure resources that are created during a deployment.A

[Functions.java file](functions-reference-java#triggers-and-annotations)in your src path that implements the function.

Files generated depend on the chosen Node.js programming model for Functions:

An HttpExample folder is created that contains:

- The
[function.json definition file](functions-reference-powershell#folder-structure) - A run.ps1 file, which contains the function code.

Files generated depend on the chosen Python programming model for Functions:

At this point, you can [run your HTTP trigger function locally](#run-functions-locally).

## Add a function to your project

You can add a new function to an existing project by using one of the predefined Functions trigger templates. To add a new function trigger, select F1 to open the command palette, then find and run the command **Azure Functions: Create Function**. Follow the prompts to choose your trigger type and define the required attributes of the trigger. If your trigger requires an access key or connection string to connect to a service, get that item ready before you create the function trigger.

This action adds a new C# class library (.cs) file to your project.

This action adds a new Java (.java) file to your project.

This action's results depend on the Node.js model version.

This action creates a new folder in the project. The folder contains a new **function.json** file and the new PowerShell code file.

This action's results depends on the Python model version.

## Connect to services

You can connect your function to other Azure services by adding input and output bindings. Bindings connect your function to other services without you having to write the connection code.

For example, the way that you define an output binding that writes data to a storage queue depends on your process model:

If necessary,

[add a reference to the package that supports your binding extension](#install-binding-extensions).Update the function method to add an attribute that defines the binding parameter, like

`QueueOutput`

for a queue output binding. You can use a`MultiResponse`

object to return multiple messages or multiple output streams.

For example, to add an output binding that writes data to a storage queue, update the function method to add a binding parameter defined by using the [ QueueOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.queueoutput) annotation. The

[object represents the messages that are written to an output binding when the function completes.](/en-us/java/api/com.microsoft.azure.functions.outputbinding)

`OutputBinding<T>`

For example, the way that you define the output binding that writes data to a storage queue depends on your Node.js model version:

Visual Studio Code lets you add bindings to your function.json file by following a convenient set of prompts.

To add a binding, open the command pallet (F1) and type **Azure Functions: add binding...**, choose the function for the new binding, and then follow the prompts, which vary depending on the type of binding being added to the function.

The following are example prompts to define a new storage output binding:

| Prompt | Value | Description |
|---|---|---|
Select binding direction |
`out` |
The binding is an output binding. |
Select binding with direction |
`Azure Queue Storage` |
The binding is an Azure Storage queue binding. |
The name used to identify this binding in your code |
`msg` |
Name that identifies the binding parameter referenced in your code. |
The queue to which the message will be sent |
`outqueue` |
The name of the queue that the binding writes to. When the queueName doesn't exist, the binding creates it on first use. |
Select setting from "local.settings.json" |
`MyStorageConnection` |
The name of an application setting that contains the connection string for the storage account. The `AzureWebJobsStorage` setting contains the connection string for the storage account you created with the function app. |

You can also right-click (Ctrl+click on macOS) directly on the **function.json** file in your function folder, select **Add binding**, and follow the same prompts.

In this example, the following binding is added to the `bindings`

array in your function.json file:

```
{
"type": "queue",
"direction": "out",
"name": "msg",
"queueName": "outqueue",
"connection": "MyStorageConnection"
}
```


For example, the way you define the output binding that writes data to a storage queue depends on your Python model version:

The following example shows the function definition after adding a [Queue Storage output binding](functions-bindings-storage-queue-output) to an [HTTP triggered function](functions-bindings-http-webhook-trigger):

Because an HTTP triggered function also returns an HTTP response, the function returns a `MultiResponse`

object, which represents both the HTTP and queue output.

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req,
FunctionContext executionContext)
{
```


This example is the definition of the `MultiResponse`

object that includes the output binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public IActionResult HttpResponse { get; set; }
}
```


When applying that example to your own project, you might need to change `HttpRequest`

to `HttpRequestData`

and `IActionResult`

to `HttpResponseData`

, depending on if you are using [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) or not.

Messages are sent to the queue when the function completes. The way you define the output binding depends on your process model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=csharp#manually-add-bindings-based-on-examples).

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=java#manually-add-bindings-based-on-examples).

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=javascript#manually-add-bindings-based-on-examples).

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=powershell#manually-add-bindings-based-on-examples).

```
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


The way you define the output binding depends on the version of your Python model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=python#manually-add-bindings-based-on-examples).

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=typescript#manually-add-bindings-based-on-examples).

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create Azure resources

Before you can publish your Functions project to Azure, you must have a function app and related resources in your Azure subscription to run your code. The function app provides an execution context for your functions. When you publish from Visual Studio Code to a function app in Azure, the project is packaged and deployed to the selected function app in your Azure subscription.

When you create a function app in Azure, you can choose either a quick function app create path using defaults or a path that gives you advanced options, such as using existing Azure resources. This way, you have more control over creating the remote resources.

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

## Create an Azure Container Apps deployment

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

Use Visual Studio Code to create Azure resources for a containerized code project. When the extension detects the presence of a Dockerfile during resource creation, it asks if you want to deploy the container image instead of just the code. Visual Studio Code creates an Azure Container Apps environment for your containerized code project that's integrated with Azure Functions. For more information, see [Azure Container Apps hosting of Azure Functions](functions-container-apps-hosting).

Note

Container deployment requires the [Azure Container Apps extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurecontainerapps). This extension is currently in preview.

The create process depends on whether you choose a quick create or you need to use advanced options:

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create Function App in Azure...`

.When prompted, choose

**Container image**.Provide the following information at the prompts:

Prompt Selection **Select subscription**(optional)Choose the subscription to use. You won't see this prompt when you have only one subscription visible under **Resources**.**Enter a name for the new function app**Type a name that's valid in a URL path. The name you type is validated to make sure that it's globally unique in Functions. **Select resource authentication type**Select **Managed identity**so that your app connects to remote resources by using Microsoft Entra ID authentication instead of using shared secrets (connection strings and keys), which are less secure.**Select a location for new resources**For better performance, choose a [region](https://azure.microsoft.com/regions/)near you.When prompted,

**Enter a name for the container app environment**.The extension shows the status of individual resources as they're being created in Azure in the

**Azure: Activity Log**panel.

For more information about the resources required to run your containerized functions in Container Apps, see [Required resources](functions-infrastructure-as-code?pivots=container-apps#required-resources).

Note

You can't currently use Visual Studio Code to deploy a containerized function app to an Azure Functions-integrated Container Apps environment. You must instead publish your container image to a container registry and then set that registry image as the deployment source for your Container Apps-hosted function app. For more information, see [Create your function app in a container](functions-how-to-custom-container#create-your-function-app-in-a-container) and [Update an image in the registry](functions-how-to-custom-container#update-an-image-in-the-registry).

## Deploy project files

Set up [continuous deployment](functions-continuous-deployment) so that your function app in Azure updates when you update source files in the connected source location. You can also deploy your project files from Visual Studio Code. When you publish from Visual Studio Code, you can take advantage of the [Zip deploy technology](functions-deployment-technologies#zip-deploy).

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Get the URL of an HTTP triggered function in Azure

To call an HTTP-triggered function from a client, you need the function's URL, which is available after deployment to your function app. This URL includes any required function keys. You can use the extension to get these URLs for your deployed functions. If you just want to run the remote function in Azure, [use the Execute function now](#run-functions-in-azure) functionality of the extension.

Select F1 to open the command palette, and then find and run the command

**Azure Functions: Copy Function URL**.Follow the prompts to select your function app in Azure and then the specific HTTP trigger that you want to invoke.


The function URL is copied to the clipboard, along with any required keys passed by the `code`

query parameter. Use an HTTP tool to submit POST requests, or a browser to submit GET requests to the remote function.

When the extension gets the URL of a function in Azure, it uses your Azure account to automatically retrieve the keys needed to start the function. [Learn more about function access keys](security-concepts#function-access-keys). Starting non-HTTP triggered functions requires using the admin key.

## Run functions

The Azure Functions extension lets you run individual functions. You can run functions either in your project on your local development computer or in your Azure subscription.

For HTTP trigger functions, the extension calls the HTTP endpoint. For other kinds of triggers, the extension calls administrator APIs to start the function. The message body of the request sent to the function depends on the trigger type. When a trigger requires test data, you're prompted to enter data in a specific JSON format.

### Run functions in Azure

To execute a function in Azure from Visual Studio Code, follow these steps:

In the command palette, enter

**Azure Functions: Execute function now**, and select your Azure subscription.From the list, choose your function app in Azure. If you don't see your function app, make sure you're signed in to the correct subscription.

From the list, choose the function that you want to run. In

**Enter request body**, type the message body of the request, and press Enter to send this request message to your function.The default text in

**Enter request body**indicates the body's format. If your function app has no functions, a notification error is shown with this error.When the function executes in Azure and returns a response, Visual Studio Code shows a notification.


You can also run your function from the **Azure: Functions** area by opening the shortcut menu for the function that you want to run from your function app in your Azure subscription, and then selecting **Execute Function Now...**.

When you run your functions in Azure from Visual Studio Code, the extension uses your Azure account to automatically retrieve the keys needed to start the function. [Learn more about function access keys](security-concepts#function-access-keys). Starting non-HTTP triggered functions requires using the admin key.

### Run functions locally

The local runtime is the same runtime that hosts your function app in Azure. The runtime reads local settings from the [local.settings.json file](#local-settings). To run your Functions project locally, you must meet [more requirements](#prerequisites).

#### Configure the project to run locally

The Functions runtime uses an Azure Storage account internally for all trigger types except HTTP and webhooks. Set the **Values.AzureWebJobsStorage** key to a valid Azure Storage account connection string.

This section uses the [Azure Storage extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage) with [Azure Storage Explorer](https://storageexplorer.com/) to connect to and retrieve the storage connection string.

To set the storage account connection string:

In Visual Studio, open

**Cloud Explorer**, expand**Storage Account**>**Your Storage Account**, then select**Properties**and copy the**Primary Connection String**value.In your project, open the local.settings.json file and set the value of the

**AzureWebJobsStorage**key to the connection string you copied.Repeat the previous step to add unique keys to the

**Values**array for any other connections required by your functions.

For more information, see [Local settings file](#local-settings).

#### Debug functions locally

To debug your functions, select F5. If [Core Tools](functions-run-local) isn't available, you're prompted to install it. When Core Tools is installed and running, output is shown in the Terminal. This step is the same as running the `func start`

Core Tools command from the Terminal, but with extra build tasks and an attached debugger.

When the project is running, you can use the **Execute Function Now...** feature of the extension to trigger your functions as you would when the project is deployed to Azure. With the project running in debug mode, breakpoints are hit in Visual Studio Code as you would expect.

In the command palette, enter

**Azure Functions: Execute function now**and choose**Local project**.Choose the function you want to run in your project and type the message body of the request in

**Enter request body**. Press Enter to send this request message to your function. The default text in**Enter request body**should indicate the format of the body. If your function app has no functions, a notification error is shown with this error.When the function runs locally and after the response is received, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.

Keys aren't required when running locally. This rule applies to both function keys and admin-level keys.

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

By default, these settings aren't migrated automatically when you publish the project to Azure. After publishing finishes, you can choose to publish settings from local.settings.json to your function app in Azure. To learn more, see [Publish application settings](#publish-application-settings).

Values in **ConnectionStrings** are never published.

Your code can read the function application settings values as environment variables. For more information, see [Environment variables](functions-dotnet-class-library#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-java#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-node#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-powershell#environment-variables).

- Your code can read the function app settings values as environment variables. For more information, see
[Environment variables](functions-reference-python#environment-variables).

## Application settings in Azure

The settings in the local.settings.json file in your project should match the application settings in the function app in Azure. You must add any new settings to both local.settings.json and the function app in Azure. These settings aren't uploaded automatically when you publish the project. Likewise, you must download any settings that you create in your function app [in the portal](functions-how-to-use-azure-function-app-settings#settings) to your local project.

### Publish application settings

The easiest way to publish the required settings to your function app in Azure is to use the **Upload settings** link that appears after you publish your project:


You can also publish settings by using the **Azure Functions: Upload Local Setting** command in the command palette. You can add individual settings to application settings in Azure by using the **Azure Functions: Add New Setting** command.

Tip

Be sure to save your local.settings.json file before you publish it.

If the local file is encrypted, the process decrypts it, publishes it, and encrypts it again. If conflicting values exist in the two locations, you're prompted to choose how to proceed.

View existing app settings in the **Azure: Functions** area by expanding your subscription, your function app, and **Application Settings**.


### Download settings from Azure

If you create application settings in Azure, you can download them into your local.settings.json file by using the **Azure Functions: Download Remote Settings** command.

As with uploading, if the local file is encrypted, the process decrypts it, updates it, and encrypts it again. If conflicting values exist in the two locations, you're prompted to choose how to proceed.

## Install binding extensions

Except for HTTP and timer triggers, bindings are implemented in extension packages.

You must explicitly install the extension packages for the triggers and bindings that need them. The specific package you install depends on your project's process model.

Run the [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to install the extension packages that you need in your project. This template demonstrates how you add a binding for an [isolated-process class library](dotnet-isolated-process-guide):

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.<BINDING_TYPE_NAME> --version <TARGET_VERSION>
```


Replace `<BINDING_TYPE_NAME>`

with the name of the package that contains the binding you need. You can find the desired binding reference article in the [list of supported bindings](functions-triggers-bindings#supported-bindings).

Replace `<TARGET_VERSION>`

in the example with a specific version of the package, such as `3.0.0-beta5`

. Valid versions are listed on the individual package pages at [NuGet.org](https://nuget.org). The major versions that correspond to the current Functions runtime are specified in the reference article for the binding.

Tip

You can also use the **NuGet** commands in [the C# Dev Kit](https://code.visualstudio.com/docs/csharp/package-management#_add-a-package) to install binding extension packages.

C# script uses [extension bundles](extension-bundles).

The easiest way to install binding extensions is to enable [extension bundles](extension-bundles). When you enable bundles, a predefined set of extension packages is automatically installed.

To enable extension bundles, open the host.json file and update its contents to match the following code:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


If for some reason you can't use an extension bundle to install binding extensions for your project, see [Explicitly install extensions](functions-bindings-register#explicitly-install-extensions).

## Monitoring functions

When you [run functions locally](#run-functions-locally), Core Tools streams log data to the Terminal console. You can also get log data when your Functions project runs in a function app in Azure. You can connect to streaming logs in Azure to see near-real-time log data. You should enable Application Insights for a more complete understanding of how your function app behaves.

### Streaming logs

When you're developing an application, it's often useful to see logging information in near-real time. You can view a stream of log files generated by your functions. Turn on logs from the command pallet with the `Azure Functions: Start streaming logs`

command. This output is an example of streaming logs for a request to an HTTP-triggered function:


To learn more, see [Streaming logs](functions-monitoring?tabs=vs-code#streaming-logs).

### Application Insights

You should monitor the execution of your functions by integrating your function app with Application Insights. When you create a function app in the Azure portal, this integration occurs by default. When you create your function app during Visual Studio publishing, you need to integrate Application Insights yourself. To learn how, see [Enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

To learn more about monitoring using Application Insights, see [Monitor Azure Functions](functions-monitoring).

## C# script projects

By default, all C# projects are created as [C# compiled class library projects](functions-dotnet-class-library). If you prefer to work with C# script projects instead, you must select C# script as the default language in the Azure Functions extension settings:

Select

**File**>**Preferences**>**Settings**.Go to

**User Settings**>**Extensions**>**Azure Functions**.Select

**C#Script**from**Azure Function: Project Language**.

After you complete these steps, calls made to the underlying Core Tools include the `--csx`

option, which generates and publishes C# script (.csx) project files. When you specify this default language, all projects that you create default to C# script projects. You're not prompted to choose a project language when a default is set. To create projects in other languages, you must change this setting or remove it from the user settings.json file. After you remove this setting, you're again prompted to choose your language when you create a project.

## Command palette reference

The Azure Functions extension provides a useful graphical interface for interacting with your function apps in Azure. The same functionality is also available as commands in the command palette (F1). These Azure Functions commands are available:

| Azure Functions command | Description |
|---|---|
Add New Settings |
Creates a new application setting in Azure. To learn more, see
|

**Configure Deployment Source**[Continuous deployment for Azure Functions](functions-continuous-deployment).**Connect to GitHub Repository****Copy Function URL**[Get the URL of the deployed function](#get-the-url-of-the-deployed-function).**Create function app in Azure**[publish to a new function app in Azure](#publish-to-azure).**Decrypt Settings**[local settings](#local-settings)that the**Azure Functions: Encrypt Settings**command encrypted.**Delete Function App**[delete the resource group](functions-add-output-binding-storage-queue-vs-code#clean-up-resources). Your local project isn't affected.**Delete Function**[republishing your project](#republish-project-files).**Delete Proxy**[Work with Azure Functions Proxies](functions-proxies).**Delete Setting****Disconnect from Repo**[continuous deployment](functions-continuous-deployment)connection between a function app in Azure and a source control repository.**Download Remote Settings****Edit settings****Encrypt settings**`Values`

array in the [local settings](#local-settings). In this file,`IsEncrypted`

is also set to `true`

, which specifies that the local runtime decrypt settings before using them. Encrypt local settings to reduce the risk of leaking valuable information. In Azure, application settings are always stored encrypted.**Execute Function Now****Initialize Project for Use with VS Code****Install or Update Azure Functions Core Tools**[Azure Functions Core Tools](functions-run-local), which is used to run functions locally.**Redeploy**[republish your project](#republish-project-files).**Rename Settings**[download those changes to the local project](#download-settings-from-azure).**Restart****Set AzureWebJobsStorage**`AzureWebJobsStorage`

application setting. This setting is required by Azure Functions. It's set when a function app is created in Azure.**Start****Start Streaming Logs**[Streaming logs](#streaming-logs).**Stop****Stop Streaming Logs****Toggle as Slot Setting****Uninstall Azure Functions Core Tools****Upload Local Settings****View Commit in GitHub****View Deployment Logs**## Next steps

To learn more about Azure Functions Core Tools, see [Work with Azure Functions Core Tools](functions-run-local).

To learn more about developing functions as .NET class libraries, see [Azure Functions C# developer reference](functions-dotnet-class-library). This article also provides links to examples of how to use attributes to declare the various types of bindings supported by Azure Functions.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-input -->

# Azure Cosmos DB input binding for Azure Functions 2.x and higher

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function. The document ID or query parameters can be determined based on the trigger that invokes the function.

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Note

When the collection is [partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions), lookup operations must also specify the partition key value.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

Unless otherwise noted, examples in this article target version 3.x of the [Azure Cosmos DB extension](functions-bindings-cosmosdb-v2). For use with extension version 4.x, you need to replace the string `collection`

in property and attribute names with `container`

.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This section contains examples that require version 3.x of Azure Cosmos DB extension and 5.x of Azure Storage extension. If not already present in your function app, add reference to the following NuGet packages:

The examples refer to a simple `ToDoItem`

type:

```
[Function(nameof(DocByIdFromJSON))]
public void DocByIdFromJSON(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[CosmosDBInput(
databaseName: "ToDoItems",
containerName: "Items",
Connection = "CosmosDBConnection",
Id = "{ToDoItemId}",
PartitionKey = "{ToDoItemPartitionKeyValue}")] ToDoItem toDoItem)
{
_logger.LogInformation($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId} Key={toDoItemLookup?.ToDoItemPartitionKeyValue}");
if (toDoItem == null)
{
_logger.LogInformation($"ToDo item not found");
}
else
{
_logger.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
}
```


### Queue trigger, look up ID from JSON

The following example shows a function that retrieves a single document. The function is triggered by a JSON message in the storage queue. The queue trigger parses the JSON into an object of type `ToDoItemLookup`

, which contains the ID and partition key value to retrieve. That ID and partition key value are used to return a `ToDoItem`

document from the specified database and collection.

```
[Function(nameof(DocByIdFromJSON))]
public void DocByIdFromJSON(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[CosmosDBInput(
databaseName: "ToDoItems",
containerName: "Items",
Connection = "CosmosDBConnection",
Id = "{ToDoItemId}",
PartitionKey = "{ToDoItemPartitionKeyValue}")] ToDoItem toDoItem)
{
_logger.LogInformation($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId} Key={toDoItemLookup?.ToDoItemPartitionKeyValue}");
if (toDoItem == null)
{
_logger.LogInformation($"ToDo item not found");
}
else
{
_logger.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
}
```


This section contains the following examples:

[HTTP trigger, look up ID from query string - String parameter](#http-trigger-look-up-id-from-query-string---string-parameter-java)[HTTP trigger, look up ID from query string - POJO parameter](#http-trigger-look-up-id-from-query-string---pojo-parameter-java)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-java)[HTTP trigger, look up ID from route data, using SqlQuery](#http-trigger-look-up-id-from-route-data-using-sqlquery-java)[HTTP trigger, get multiple docs from route data, using SqlQuery](#http-trigger-get-multiple-docs-from-route-data-using-sqlquery-java)

The examples refer to a simple `ToDoItem`

type:

```
public class ToDoItem {
private String id;
private String description;
public String getId() {
return id;
}
public String getDescription() {
return description;
}
@Override
public String toString() {
return "ToDoItem={id=" + id + ",description=" + description + "}";
}
}
```


### HTTP trigger, look up ID from query string - String parameter

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a document from the specified database and collection, in String form.

```
public class DocByIdFromQueryString {
@FunctionName("DocByIdFromQueryString")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
id = "{Query.id}",
partitionKey = "{Query.partitionKeyValue}",
connectionStringSetting = "Cosmos_DB_Connection_String")
Optional<String> item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("String from the database is " + (item.isPresent() ? item.get() : null));
// Convert and display
if (!item.isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from Cosmos. Alternatively, we can parse the JSON string
// and return an enriched JSON object.
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item.get())
.build();
}
}
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBInput`

annotation on function parameters whose value would come from Azure Cosmos DB. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

### HTTP trigger, look up ID from query string - POJO parameter

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value used to retrieve a document from the specified database and collection. The document is then converted to an instance of the `ToDoItem`

POJO previously created, and passed as an argument to the function.

```
public class DocByIdFromQueryStringPojo {
@FunctionName("DocByIdFromQueryStringPojo")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
id = "{Query.id}",
partitionKey = "{Query.partitionKeyValue}",
connectionStringSetting = "Cosmos_DB_Connection_String")
ToDoItem item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("Item from the database is " + item);
// Convert and display
if (item == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item)
.build();
}
}
}
```


### HTTP trigger, look up ID from route data

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a route parameter to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a document from the specified database and collection, returning it as an `Optional<String>`

.

```
public class DocByIdFromRoute {
@FunctionName("DocByIdFromRoute")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "todoitems/{partitionKeyValue}/{id}")
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
id = "{id}",
partitionKey = "{partitionKeyValue}",
connectionStringSetting = "Cosmos_DB_Connection_String")
Optional<String> item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("String from the database is " + (item.isPresent() ? item.get() : null));
// Convert and display
if (!item.isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from Cosmos. Alternatively, we can parse the JSON string
// and return an enriched JSON object.
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item.get())
.build();
}
}
}
```


### HTTP trigger, look up ID from route data, using SqlQuery

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a route parameter to specify the ID to look up. That ID is used to retrieve a document from the specified database and collection, converting the result set to a `ToDoItem[]`

, since many documents may be returned, depending on the query criteria.

Note

If you need to query by just the ID, it is recommended to use a lookup, like the [previous examples](#http-trigger-look-up-id-from-query-string---pojo-parameter-java), as it consumes less [request units](/en-us/azure/cosmos-db/request-units). Point read operations (GET) are [more efficient](/en-us/azure/cosmos-db/optimize-cost-reads-writes) than queries by ID.

```
public class DocByIdFromRouteSqlQuery {
@FunctionName("DocByIdFromRouteSqlQuery")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "todoitems2/{id}")
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
sqlQuery = "select * from Items r where r.id = {id}",
connectionStringSetting = "Cosmos_DB_Connection_String")
ToDoItem[] item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("Items from the database are " + item);
// Convert and display
if (item == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item)
.build();
}
}
}
```


### HTTP trigger, get multiple docs from route data, using SqlQuery

The following example shows a Java function that retrieves multiple documents. The function is triggered by an HTTP request that uses a route parameter `desc`

to specify the string to search for in the `description`

field. The search term is used to retrieve a collection of documents from the specified database and collection, converting the result set to a `ToDoItem[]`

and passing it as an argument to the function.

```
public class DocsFromRouteSqlQuery {
@FunctionName("DocsFromRouteSqlQuery")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "todoitems3/{desc}")
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
sqlQuery = "select * from Items r where contains(r.description, {desc})",
connectionStringSetting = "Cosmos_DB_Connection_String")
ToDoItem[] items,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("Number of items from the database is " + (items == null ? 0 : items.length));
// Convert and display
if (items == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("No documents found.")
.build();
}
else {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(items)
.build();
}
}
}
```


This section contains the following examples that read a single document by specifying an ID value from various sources:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-typescript)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-typescript)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-typescript)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-typescript)

### Queue trigger, look up ID from JSON

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that reads a single document and updates the document's text value.

```
import { app, input, InvocationContext, output } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
id: '{queueTrigger}',
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: false,
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
interface MyDocument {
text: string;
}
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
const doc = <MyDocument>context.extraInputs.get(cosmosInput);
doc.text = 'This was updated!';
context.extraOutputs.set(cosmosOutput, doc);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
extraOutputs: [cosmosOutput],
handler: storageQueueTrigger1,
});
```


### HTTP trigger, look up ID from query string

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{Query.id}',
partitionKey: '{Query.partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
interface ToDoDocument {
description: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const toDoItem = <ToDoDocument>context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.description}`,
};
}
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [cosmosInput],
handler: httpTrigger1,
});
```


### HTTP trigger, look up ID from route data

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{id}',
partitionKey: '{partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
interface ToDoDocument {
description: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const toDoItem = <ToDoDocument>context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.description}`,
};
}
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'todoitems/{partitionKeyValue}/{id}',
extraInputs: [cosmosInput],
handler: httpTrigger1,
});
```


### Queue trigger, get multiple docs, using SqlQuery

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

```
import { app, input, InvocationContext } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'MyDb',
collectionName: 'MyCollection',
sqlQuery: 'SELECT * from c where c.departmentId = {departmentId}',
connectionStringSetting: 'CosmosDBConnection',
});
interface MyDocument {}
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
const documents = <MyDocument[]>context.extraInputs.get(cosmosInput);
for (const document of documents) {
// operate on each document
}
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
handler: storageQueueTrigger1,
});
```


This section contains the following examples that read a single document by specifying an ID value from various sources:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-javascript)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-javascript)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-javascript)

### Queue trigger, look up ID from JSON

The following example shows a [JavaScript function](functions-reference-node) that reads a single document and updates the document's text value.

```
const { app, input, output } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
id: '{queueTrigger}',
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: false,
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
extraOutputs: [cosmosOutput],
handler: (queueItem, context) => {
const doc = context.extraInputs.get(cosmosInput);
doc.text = 'This was updated!';
context.extraOutputs.set(cosmosOutput, doc);
},
});
```


### HTTP trigger, look up ID from query string

The following example shows a [JavaScript function](functions-reference-node) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
const { app, input } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{Query.id}',
partitionKey: '{Query.partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [cosmosInput],
handler: (request, context) => {
const toDoItem = context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.Description}`,
};
}
},
});
```


### HTTP trigger, look up ID from route data

The following example shows a [JavaScript function](functions-reference-node) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
const { app, input } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{id}',
partitionKey: '{partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'todoitems/{partitionKeyValue}/{id}',
extraInputs: [cosmosInput],
handler: (request, context) => {
const toDoItem = context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.Description}`,
};
}
},
});
```


### Queue trigger, get multiple docs, using SqlQuery

The following example shows a [JavaScript function](functions-reference-node) that retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

```
const { app, input } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'MyDb',
collectionName: 'MyCollection',
sqlQuery: 'SELECT * from c where c.departmentId = {departmentId}',
connectionStringSetting: 'CosmosDBConnection',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
handler: (queueItem, context) => {
const documents = context.extraInputs.get(cosmosInput);
for (const document of documents) {
// operate on each document
}
},
});
```


[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-ps)[HTTP trigger, look up ID from query string](#http-trigger-id-query-string-ps)[HTTP trigger, look up ID from route data](#http-trigger-id-route-data-ps)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-multiple-docs-sqlquery-ps)

### Queue trigger, look up ID from JSON

The following example demonstrates how to read and update a single Azure Cosmos DB document. The document's unique identifier is provided through JSON value in a queue message.

The Azure Cosmos DB input binding is listed first in the list of bindings found in the function's configuration file (*function.json*).

```
{
"name": "InputDocumentIn",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"id": "{queueTrigger_payload_property}",
"partitionKey": "{queueTrigger_payload_property}",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in"
},
{
"name": "InputDocumentOut",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": false,
"partitionKey": "{queueTrigger_payload_property}",
"connectionStringSetting": "CosmosDBConnection",
"direction": "out"
}
```


The *run.ps1* file has the PowerShell code which reads the incoming document and outputs changes.

```
param($QueueItem, $InputDocumentIn, $TriggerMetadata)
$Document = $InputDocumentIn
$Document.text = 'This was updated!'
Push-OutputBinding -Name InputDocumentOut -Value $Document
```


### HTTP trigger, look up ID from query string

The following example demonstrates how to read and update a single Azure Cosmos DB document from a web API. The document's unique identifier is provided through a querystring parameter from the HTTP request, as defined in the binding's `"Id": "{Query.Id}"`

property.

The Azure Cosmos DB input binding is listed first in the list of bindings found in the function's configuration file (*function.json*).

```
{
"bindings": [
{
"type": "cosmosDB",
"name": "ToDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"Id": "{Query.id}",
"PartitionKey": "{Query.partitionKeyValue}"
},
{
"authLevel": "anonymous",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "Response",
"type": "http",
"direction": "out"
},
],
"disabled": false
}
```


The *run.ps1* file has the PowerShell code which reads the incoming document and outputs changes.

```
using namespace System.Net
param($Request, $ToDoItem, $TriggerMetadata)
Write-Host 'PowerShell HTTP trigger function processed a request'
if (-not $ToDoItem) {
Write-Host 'ToDo item not found'
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::NotFound
Body = $ToDoItem.Description
})
} else {
Write-Host "Found ToDo item, Description=$($ToDoItem.Description)"
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $ToDoItem.Description
})
}
```


### HTTP trigger, look up ID from route data

The following example demonstrates how to read and update a single Azure Cosmos DB document from a web API. The document's unique identifier is provided through a route parameter. The route parameter is defined in the HTTP request binding's `route`

property and referenced in the Azure Cosmos DB `"Id": "{Id}"`

binding property.

The Azure Cosmos DB input binding is listed first in the list of bindings found in the function's configuration file (*function.json*).

```
{
"bindings": [
{
"type": "cosmosDB",
"name": "ToDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"Id": "{id}",
"PartitionKey": "{partitionKeyValue}"
},
{
"authLevel": "anonymous",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
],
"route": "todoitems/{partitionKeyValue}/{id}"
},
{
"name": "Response",
"type": "http",
"direction": "out"
}
],
"disabled": false
}
```


The *run.ps1* file has the PowerShell code which reads the incoming document and outputs changes.

```
using namespace System.Net
param($Request, $ToDoItem, $TriggerMetadata)
Write-Host 'PowerShell HTTP trigger function processed a request'
if (-not $ToDoItem) {
Write-Host 'ToDo item not found'
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::NotFound
Body = $ToDoItem.Description
})
} else {
Write-Host "Found ToDo item, Description=$($ToDoItem.Description)"
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $ToDoItem.Description
})
}
```


### Queue trigger, get multiple docs, using SqlQuery

The following example demonstrates how to read multiple Azure Cosmos DB documents. The function's configuration file (*function.json*) defines the binding properties, which includes the `sqlQuery`

. The SQL statement provided to the `sqlQuery`

property selects the set of documents provided to the function.

```
{
"name": "Documents",
"type": "cosmosDB",
"direction": "in",
"databaseName": "MyDb",
"collectionName": "MyCollection",
"sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
"connectionStringSetting": "CosmosDBConnection"
}
```


The *run1.ps1* file has the PowerShell code which reads the incoming documents.

```
param($QueueItem, $Documents, $TriggerMetadata)
foreach ($Document in $Documents) {
# operate on each document
}
```


This section contains the following examples that read a single document by specifying an ID value from various sources:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-python)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-python)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-python)

The examples depend on whether you use the [v1 or v2 Python programming model](functions-reference-python).

### Using SDK-Type Bindings for Cosmos DB (Preview)

This example uses SDK types to directly access the underlying [ CosmosClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_cosmosclient/function_app.py) object provided by the Cosmos DB input binding:

The function loops through all the databases and logs their IDs.

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.cosmosdb as cosmos
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="cosmos")
@app.cosmos_db_input(arg_name="client",
connection="CosmosDBConnection",
database_name=None,
container_name=None)
def get_docs(req: func.HttpRequest, client: cosmos.CosmosClient):
databases = client.list_databases()
for db in databases:
logging.info(f"Found database with ID: {db.get('id')}")
return "ok"
```


For examples of using other SDK types, see the [ ContainerProxy](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_containerproxy/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_databaseproxy/function_app.py)

`DatabaseProxy`

[Python SDK Bindings for CosmosDB Sample](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

### Queue trigger, look up ID from JSON

The following example shows an Azure Cosmos DB input binding. The function reads a single document and updates the document's text value.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.queue_trigger(arg_name="msg",
queue_name="outqueue",
connection="AzureWebJobsStorage")
@app.cosmos_db_input(arg_name="documents",
database_name="MyDatabase",
collection_name="MyCollection",
id="{msg.payload_property}",
partition_key="{msg.payload_property}",
connection_string_setting="MyAccount_COSMOSDB")
@app.cosmos_db_output(arg_name="outputDocument",
database_name="MyDatabase",
collection_name="MyCollection",
connection_string_setting="MyAccount_COSMOSDB")
def test_function(msg: func.QueueMessage,
inputDocument: func.DocumentList,
outputDocument: func.Out[func.Document]):
doc = inputDocument[0]
doc["text"] = "This was updated!"
outputDocument.set(doc)
print(f"Updated document.")
```


### HTTP trigger, look up ID from query string

The following example shows a function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

### HTTP trigger, look up ID from route data

The following example shows a function that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

### Queue trigger, get multiple docs, using SqlQuery

The following example shows an Azure Cosmos DB input binding Python function that uses the binding. The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-input).

| Attribute property | Description |
|---|---|
Connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being queried. For more information, see
|

**DatabaseName****ContainerName****PartitionKey**[partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions)containers.**Id**[binding expressions](functions-bindings-expressions-patterns). Don't set both the`Id`

and `SqlQuery`

properties. If you don't set either one, the entire container is retrieved.**SqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the `Id`

and `SqlQuery`

properties. If you don't set either one, the entire container is retrieved.**PreferredLocations**`East US,South Central US,North Europe`

.## Decorators

*Applies only to the Python v2 programming model.*

Python v2 functions are defined using the `cosmos_db_input`

decorator, which supports these properties, depending on the extension version:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the collection being monitored. |
`container_name` |
The name of the Azure Cosmos DB collection being monitored. |
`connection` |
The connection string of the Azure Cosmos DB being monitored. |
`partition_key` |
The partition key of the Azure Cosmos DB being monitored. |
`id` |
The ID of the document to retrieve. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBInput`

annotation on parameters that read from Azure Cosmos DB. The annotation supports the following properties:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property | Description |
|---|---|
type |
Must be set to `cosmosDB` . |
direction |
Must be set to `in` . |
name |
The variable name used in function code that represents the list of documents with changes. |
connection |
The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****partitionKey**[partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions)containers.**id**[binding expressions](functions-bindings-expressions-patterns). Don't set both the`id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**sqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the `id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**preferredLocations**`East US,South Central US,North Europe`

.See the [Example section](#example) for complete examples.

## Usage

When the function exits successfully, any changes made to the input document are automatically persisted.

The parameter type supported by the Cosmos DB input binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single document, the Cosmos DB input binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions attempts to deserialize the JSON data of the document into a plain-old CLR object (POCO) type. |

When you want the function to process multiple documents from a query, the Cosmos DB input binding can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities returned by the query. Each entry represents one document. |
1 |

[Database](/en-us/dotnet/api/microsoft.azure.cosmos.database)1[Container](/en-us/dotnet/api/microsoft.azure.cosmos.container)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.CosmosDB 4.4.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.CosmosDB/4.4.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), the [@CosmosDBInput](/en-us/java/api/com.microsoft.azure.functions.annotation.cosmosdbinput) annotation exposes Azure Cosmos DB data to the function. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

Updates to documents are not made automatically upon function exit. To update documents in a function use an [output binding](functions-bindings-cosmosdb-v2-input). See the [PowerShell example](#example) for more detail.

Data is made available to the function via a `DocumentList`

parameter. Changes made to the document are not automatically persisted.
Functions also support Python SDK type bindings for Azure Cosmos, which lets you work with data using these underlying SDK types:

Important

Support for CosmosDB SDK types for Python is in Preview and is only supported for the Python v2 programming model. For more information, see

[SDK types in Python].

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections). This option is only available for the`connection`

and`leaseConnection`

versions from[version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Account Endpoint | `<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. | https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles1 |
|---|---|
Trigger2 |
|

[Cosmos DB Built-in Data Reader](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)[Cosmos DB Built-in Data Contributor](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.
