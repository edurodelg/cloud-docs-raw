---
merged_at: 2026-01-26T23:29:57.714452
merged_files: 2
---


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
