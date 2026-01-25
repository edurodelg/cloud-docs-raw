---
merged_at: 2026-01-25T15:41:11.634441
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-kafka-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-trigger -->

# Apache Kafka trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the Apache Kafka trigger in Azure Functions to run your function code in response to messages in Kafka topics. You can also use a [Kafka output binding](functions-bindings-kafka-output) to write from your function to a topic. For information on setup and configuration details, see [Apache Kafka bindings for Azure Functions overview](functions-bindings-kafka).

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

The usage of the trigger depends on the C# modality used in your function app, which can be one of the following modes:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example shows a C# function that reads and logs the Kafka message as a Kafka event:

```
[Function("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(eventData)["Value"]}");
}
```


To receive events in a batch, use a string array as input, as shown in the following example:

```
[Function("KafkaTriggerMany")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
IsBatched = true)] string[] events, FunctionContext context)
{
foreach (var kevent in events)
{
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {JObject.Parse(kevent)["Value"]}");
}
```


The following function logs the message and headers for the Kafka Event:

```
[Function("KafkaTriggerWithHeaders")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default")] string eventData, FunctionContext context)
{
var eventJsonObject = JObject.Parse(eventData);
var logger = context.GetLogger("KafkaFunction");
logger.LogInformation($"C# Kafka trigger function processed a message: {eventJsonObject["Value"]}");
var headersJArr = eventJsonObject["Headers"] as JArray;
logger.LogInformation("Headers for this event: ");
foreach (JObject header in headersJArr)
{
logger.LogInformation($"{header["Key"]} {System.Text.Encoding.UTF8.GetString((byte[])header["Value"])}");
}
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/).

The usage of the trigger depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your trigger directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
const { app } = require("@azure/functions");
async function kafkaTrigger(event, context) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Key: " + event.Key);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
const { app } = require("@azure/functions");
async function kafkaTriggerMany(events, context) {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Key: " + event.Key);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
const { app } = require("@azure/functions");
async function kafkaAvroGenericTrigger(event, context) {
context.log("Processed kafka event: ", event);
if (context.triggerMetadata?.key !== undefined) {
context.log("message key: ", context.triggerMetadata?.key);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
password: "EventHubConnectionString",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
username: "$ConnectionString",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
export async function kafkaTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
app.generic("Kafkatrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string"
},
handler: kafkaTrigger,
});
```


To receive events in a batch, set the `cardinality`

value to `many`

, as shown in these examples:

```
import { app, InvocationContext } from "@azure/functions";
// This is a sample interface that describes the actual data in your event.
interface EventData {
registertime: number;
userid: string;
regionid: string;
gender: string;
}
interface KafkaEvent {
Offset: number;
Partition: number;
Topic: string;
Timestamp: number;
Value: string;
}
export async function kafkaTriggerMany(
events: any,
context: InvocationContext
): Promise<void> {
for (const event of events) {
context.log("Event Offset: " + event.Offset);
context.log("Event Partition: " + event.Partition);
context.log("Event Topic: " + event.Topic);
context.log("Event Timestamp: " + event.Timestamp);
context.log("Event Value (as string): " + event.Value);
let event_obj: EventData = JSON.parse(event.Value);
context.log("Event Value Object: ");
context.log(" Value.registertime: ", event_obj.registertime.toString());
context.log(" Value.userid: ", event_obj.userid);
context.log(" Value.regionid: ", event_obj.regionid);
context.log(" Value.gender: ", event_obj.gender);
}
}
app.generic("kafkaTriggerMany", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
topic: "topic",
brokerList: "%BrokerList%",
username: "%ConfluentCloudUserName%",
password: "%ConfluentCloudPassword%",
consumerGroup: "$Default",
protocol: "saslSsl",
authenticationMode: "plain",
dataType: "string",
cardinality: "MANY"
},
handler: kafkaTriggerMany,
});
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. This example defines the trigger for the specific provider with a generic Avro schema:

```
import { app, InvocationContext } from "@azure/functions";
export async function kafkaAvroGenericTrigger(
event: any,
context: InvocationContext
): Promise<void> {
context.log("Processed kafka event: ", event);
context.log(
`Message ID: ${event.id}, amount: ${event.amount}, type: ${event.type}`
);
if (context.triggerMetadata?.key !== undefined) {
context.log(`Message Key : ${context.triggerMetadata?.key}`);
}
}
app.generic("kafkaAvroGenericTrigger", {
trigger: {
type: "kafkaTrigger",
direction: "in",
name: "event",
protocol: "SASLSSL",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
dataType: "string",
topic: "topic",
authenticationMode: "PLAIN",
avroSchema:
'{"type":"record","name":"Payment","namespace":"io.confluent.examples.clients.basicavro","fields":[{"name":"id","type":"string"},{"name":"amount","type":"double"},{"name":"type","type":"string"}]}',
consumerGroup: "$Default",
brokerList: "%BrokerList%",
},
handler: kafkaAvroGenericTrigger,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the `function.json`

file depend on your event provider. In these examples, the event providers are either Confluent or Azure Event Hubs. The following examples show a Kafka trigger for a function that reads and logs a Kafka message.

The following `function.json`

file defines the trigger for the specific provider:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


To receive events in a batch, set the `cardinality`

value to `many`

in the function.json file, as shown in the following examples:

```
{
"bindings": [
{
"type": "kafkaTrigger",
"name": "kafkaEvent",
"direction": "in",
"protocol" : "SASLSSL",
"password" : "%ConfluentCloudPassword%",
"dataType" : "string",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"cardinality" : "MANY",
"consumerGroup" : "$Default",
"username" : "%ConfluentCloudUserName%",
"brokerList" : "%BrokerList%",
"sslCaLocation": "confluent_cloud_cacert.pem"
}
]
}
```


The following code parses the array of events and logs the event data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
$kafkaEvents
foreach ($kafkaEvent in $kafkaEvents) {
$event = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $event.Value"
}
```


The following code logs the header data:

```
using namespace System.Net
param($kafkaEvents, $TriggerMetadata)
foreach ($kafkaEvent in $kafkaEvents) {
$kevent = $kafkaEvent | ConvertFrom-Json -AsHashtable
Write-Output "Powershell Kafka trigger function called for message $kevent.Value"
Write-Output "Headers for this message:"
foreach ($header in $kevent.Headers) {
$DecodedValue = [System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String($header.Value))
$Key = $header.Key
Write-Output "Key: $Key Value: $DecodedValue"
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function.json defines the trigger for the specific provider with a generic Avro schema:

```
{
"bindings" : [ {
"type" : "kafkaTrigger",
"direction" : "in",
"name" : "kafkaEvent",
"protocol" : "SASLSSL",
"password" : "ConfluentCloudPassword",
"topic" : "topic",
"authenticationMode" : "PLAIN",
"avroSchema" : "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}",
"consumerGroup" : "$Default",
"username" : "ConfluentCloudUsername",
"brokerList" : "%BrokerList%"
} ]
}
```


The following code runs when the function is triggered:

```
using namespace System.Net
param($kafkaEvent, $TriggerMetadata)
Write-Output "Powershell Kafka trigger function called for message $kafkaEvent.Value"
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the trigger depends on your version of the Python programming model.

In the Python v2 model, you define your trigger directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show how to define a Kafka trigger for a function that reads a Kafka message.

```
@KafkaTrigger.function_name(name="KafkaTrigger")
@KafkaTrigger.kafka_trigger(
arg_name="kevent",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default1")
def kafka_trigger(kevent : func.KafkaEvent):
logging.info(kevent.get_body().decode('utf-8'))
logging.info(kevent.metadata)
```


This example receives events in a batch by setting the `cardinality`

value to `many`

.

```
@KafkaTrigger.function_name(name="KafkaTriggerMany")
@KafkaTrigger.kafka_trigger(
arg_name="kevents",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
cardinality="MANY",
data_type="string",
consumer_group="$Default2")
def kafka_trigger_many(kevents : typing.List[func.KafkaEvent]):
for event in kevents:
logging.info(event.get_body())
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger.

```
@KafkaTriggerAvro.function_name(name="KafkaTriggerAvroOne")
@KafkaTriggerAvro.kafka_trigger(
arg_name="kafkaTriggerAvroGeneric",
topic="KafkaTopic",
broker_list="KafkaBrokerList",
username="KafkaUsername",
password="KafkaPassword",
protocol="SaslSsl",
authentication_mode="Plain",
consumer_group="$Default",
avro_schema= "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}")
def kafka_trigger_avro_one(kafkaTriggerAvroGeneric : func.KafkaEvent):
logging.info(kafkaTriggerAvroGeneric.get_body().decode('utf-8'))
logging.info(kafkaTriggerAvroGeneric.metadata)
```


For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure your trigger depend on the specific event provider.

The following example shows a Java function that reads and logs the content of the Kafka event:

```
@FunctionName("KafkaTrigger")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string"
) String kafkaEventData,
final ExecutionContext context) {
context.getLogger().info(kafkaEventData);
}
```


To receive events in a batch, use an input string as an array, as shown in the following example:

```
@FunctionName("KafkaTriggerMany")
public void runMany(
@KafkaTrigger(
name = "kafkaTriggerMany",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
cardinality = Cardinality.MANY,
dataType = "string"
) String[] kafkaEvents,
final ExecutionContext context) {
for (String kevent: kafkaEvents) {
context.getLogger().info(kevent);
}
}
```


The following function logs the message and headers for the Kafka Event:

```
@FunctionName("KafkaTriggerManyWithHeaders")
public void runSingle(
@KafkaTrigger(
name = "KafkaTrigger",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
dataType = "string",
cardinality = Cardinality.MANY
) List<String> kafkaEvents,
final ExecutionContext context) {
Gson gson = new Gson();
for (String keventstr: kafkaEvents) {
KafkaEntity kevent = gson.fromJson(keventstr, KafkaEntity.class);
context.getLogger().info("Java Kafka trigger function called for message: " + kevent.Value);
context.getLogger().info("Headers for the message:");
for (KafkaHeaders header : kevent.Headers) {
String decodedValue = new String(Base64.getDecoder().decode(header.Value));
context.getLogger().info("Key:" + header.Key + " Value:" + decodedValue);
}
}
}
```


You can define a generic [Avro schema](http://avro.apache.org/docs/current/) for the event passed to the trigger. The following function defines a trigger for the specific provider with a generic Avro schema:

```
private static final String schema = "{\"type\":\"record\",\"name\":\"Payment\",\"namespace\":\"io.confluent.examples.clients.basicavro\",\"fields\":[{\"name\":\"id\",\"type\":\"string\"},{\"name\":\"amount\",\"type\":\"double\"},{\"name\":\"type\",\"type\":\"string\"}]}";
@FunctionName("KafkaAvroGenericTrigger")
public void runOne(
@KafkaTrigger(
name = "kafkaAvroGenericSingle",
topic = "topic",
brokerList="%BrokerList%",
consumerGroup="$Default",
username = "ConfluentCloudUsername",
password = "ConfluentCloudPassword",
avroSchema = schema,
authenticationMode = BrokerAuthenticationMode.PLAIN,
protocol = BrokerProtocol.SASLSSL) Payment payment,
final ExecutionContext context) {
context.getLogger().info(payment.toString());
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `KafkaTriggerAttribute`

to define the function trigger.

The following table explains the properties you can set by using this trigger attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**Topic****ConsumerGroup****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**AuthenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

, and `OAuthBearer`

.**Username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**SslCaLocation****SslCertificateLocation****SslKeyLocation****SslKeyPassword****SslCertificatePEM**[Connections](#connections)for more information.**SslKeyPEM**[Connections](#connections)for more information.**SslCaPEM**[Connections](#connections)for more information.**SslCertificateandKeyPEM**[Connections](#connections)for more information.**SchemaRegistryUrl**[Connections](#connections)for more information.**SchemaRegistryUsername**[Connections](#connections)for more information.**SchemaRegistryPassword**[Connections](#connections)for more information.**OAuthBearerMethod**`oidc`

and `default`

.**OAuthBearerClientId**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**OAuthBearerClientSecret**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**OAuthBearerScope****OAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.**OAuthBearerExtensions**`oidc`

method is used. For example: `supportFeatureX=true,organizationId=sales-emea`

.## Annotations

The `KafkaTrigger`

annotation enables you to create a function that runs when it receives a topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
(Required) The name of the variable that represents the queue or topic message in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `dataType`

.**dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual byte array parameter type.**consumerGroup****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**lagThreshold****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

and `default`

.**oAuthBearerClientId**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**oAuthBearerClientSecret**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**oAuthBearerScope****oAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. Python uses snake_case naming conventions for configuration properties.

function.json property |
Description |
|---|---|
type |
(Required) Set to `kafkaTrigger` . |
direction |
(Required) Set to `in` . |
name |
(Required) The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers monitored by the trigger. See
|

**topic****cardinality**`ONE`

(default) and `MANY`

. Use `ONE`

when the input is a single message and `MANY`

when the input is an array of messages. When you use `MANY`

, you must also set a `data_type`

.**data_type**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**consumerGroup****avroSchema****authentication_mode**`NOTSET`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NOTSET`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****lag_threshold****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The Kafka trigger currently supports Kafka events as strings and string arrays that are JSON payloads.

The Kafka trigger passes Kafka messages to the function as strings. The trigger also supports string arrays that are JSON payloads.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

You can't use the **Test/Run** feature of the **Code + Test** page in the Azure portal to work with Kafka triggers. You must instead send test events directly to the topic being monitored by the trigger.

For a complete set of supported host.json settings for the Kafka trigger, see [host.json settings](functions-bindings-kafka#hostjson-settings).

## Connections

Store all connection information required by your triggers and bindings in application settings, not in the binding definitions in your code. This guidance applies to credentials, which you should never store in your code.

Important

Credential settings must reference an [application setting](functions-how-to-use-azure-function-app-settings#settings). Don't hard-code credentials in your code or configuration files. When running locally, use the [local.settings.json file](functions-develop-local#local-settings-file) for your credentials, and don't publish the local.settings.json file.

When connecting to a managed Kafka cluster provided by [Confluent in Azure](https://www.confluent.io/azure/), you can use one of the following authentication methods.

Note

When using the Flex Consumption plan, file location-based certificate authentication properties (`SslCaLocation`

, `SslCertificateLocation`

, `SslKeyLocation`

) aren't supported. Instead, use the PEM-based certificate properties (`SslCaPEM`

, `SslCertificatePEM`

, `SslKeyPEM`

, `SslCertificateandKeyPEM`

) or store certificates in Azure Key Vault.

#### Schema Registry

To make use of schema registry provided by Confluent in Kafka Extension, set the following credentials:

| Setting | Recommended Value | Description |
|---|---|---|
SchemaRegistryUrl |
`SchemaRegistryUrl` |
URL of the schema registry service used for schema management. Usually of the format `https://psrc-xyz.us-east-2.aws.confluent.cloud` |
SchemaRegistryUsername |
`CONFLUENT_API_KEY` |
Username for basic auth on schema registry (if required). |
SchemaRegistryPassword |
`CONFLUENT_API_SECRET` |
Password for basic auth on schema registry (if required). |

#### Username/Password authentication

While using this form of authentication, make sure that `Protocol`

is set to either `SaslPlaintext`

or `SaslSsl`

, `AuthenticationMode`

is set to `Plain`

, `ScramSha256`

or `ScramSha512`

and, if the CA cert being used is different from the default ISRG Root X1 cert, make sure to update `SslCaLocation`

or `SslCaPEM`

.

| Setting | Recommended value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
Username |
`ConfluentCloudUsername` |
App setting named `ConfluentCloudUsername` contains the API access key from the Confluent Cloud web site. |
Password |
`ConfluentCloudPassword` |
App setting named `ConfluentCloudPassword` contains the API secret obtained from the Confluent Cloud web site. |
SslCaPEM |
`SSLCaPemCertificate` |
App setting named `SSLCaPemCertificate` that contains the CA certificate as a string in PEM format. The value should follow the standard format, for example: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----` . |

#### SSL authentication

Ensure that `Protocol`

is set to `SSL`

.

| Setting | Recommended Value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
SslCaPEM |
`SslCaCertificatePem` |
App setting named `SslCaCertificatePem` that contains PEM value of the CA certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslCertificatePEM |
`SslClientCertificatePem` |
App setting named `SslClientCertificatePem` that contains PEM value of the client certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslKeyPEM |
`SslClientKeyPem` |
App setting named `SslClientKeyPem` that contains PEM value of the client private key as a string. The value should follow the standard format: `-----BEGIN PRIVATE KEY-----\nMII...JQ==\n-----END PRIVATE KEY-----` |
SslCertificateandKeyPEM |
`SslClientCertificateAndKeyPem` |
App setting named `SslClientCertificateAndKeyPem` that contains PEM value of the client certificate and client private key concatenated as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----\n-----BEGIN PRIVATE KEY-----\nMIIE....BM=\n-----END PRIVATE KEY-----` |
SslKeyPassword |
`SslClientKeyPassword` |
App setting named `SslClientKeyPassword` that contains the password for the private key (if any). |

#### OAuth authentication

When using OAuth authentication, configure the OAuth-related properties in your binding definitions.

The string values you use for these settings must be present as [application settings in Azure](functions-how-to-use-azure-function-app-settings#settings) or in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file) during local development.

You should also set the `Protocol`

and `AuthenticationMode`

in your binding definitions.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-blob-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-trigger -->

# Azure Blob storage trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Blob storage trigger starts a function when a new or updated blob is detected. The blob contents are provided as [input to the function](functions-bindings-storage-blob-input).

Tip

There are several ways to execute your function code based on changes to blobs in a storage container. If you choose to use the Blob storage trigger, there are two implementations offered: a polling-based one (referenced in this article) and an event-based one. It is recommended that you use the [event-based implementation](functions-event-grid-blob-trigger) as it has lower latency than the other. Also, the Flex Consumption plan supports only the event-based Blob storage trigger.

For details about differences between the two implementations of the Blob storage trigger, as well as other triggering options, see

[Working with blobs].

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
```


This function uses a byte array to write a log when a blob is added or updated in the `myblob`

container.

```
@FunctionName("blobprocessor")
public void run(
@BlobTrigger(name = "file",
dataType = "binary",
path = "myblob/{name}",
connection = "MyStorageAccountAppSetting") byte[] content,
@BindingName("name") String filename,
final ExecutionContext context
) {
context.getLogger().info("Name: " + filename + " Size: " + content.length + " bytes");
}
```


This [SDK types example](functions-reference-java#sdk-types) uses `BlobClient`

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


This [SDK types example](functions-reference-java#sdk-types) uses `BlobContainerClient`

to access info about blobs in the container that triggered the function.

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


This [SDK types example](functions-reference-java#sdk-types) uses `BlobClient`

to get information from the input binding about the blob that triggered the execution.

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


The following example shows a blob trigger [TypeScript code](functions-reference-node). The function writes a log when a blob is added or updated in the `samples-workitems`

container.

The string `{name}`

in the blob trigger path `samples-workitems/{name}`

creates a [binding expression](functions-bindings-expressions-patterns) that you can use in function code to access the file name of the triggering blob. For more information, see [Blob name patterns](#blob-name-patterns) later in this article.

```
import { app, InvocationContext } from '@azure/functions';
export async function storageBlobTrigger1(blob: Buffer, context: InvocationContext): Promise<void> {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
}
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
handler: storageBlobTrigger1,
});
```


The following example shows a blob trigger [JavaScript code](functions-reference-node). The function writes a log when a blob is added or updated in the `samples-workitems`

container.

The string `{name}`

in the blob trigger path `samples-workitems/{name}`

creates a [binding expression](functions-bindings-expressions-patterns) that you can use in function code to access the file name of the triggering blob. For more information, see [Blob name patterns](#blob-name-patterns) later in this article.

```
const { app } = require('@azure/functions');
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
handler: (blob, context) => {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
},
});
```


The following example demonstrates how to create a function that runs when a file is added to `source`

blob storage container.

The function configuration file (*function.json*) includes a binding with the `type`

of `blobTrigger`

and `direction`

set to `in`

.

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "source/{name}",
"connection": "MyStorageAccountConnectionString"
}
]
}
```


Here's the associated code for the *run.ps1* file.

```
param([byte[]] $InputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger: Name: $($TriggerMetadata.Name) Size: $($InputBlob.Length) bytes"
```


This example uses SDK types to directly access the underlying [ BlobClient](/en-us/python/api/azure-storage-blob/azure.storage.blob.blobclient) object provided by the Blob storage trigger:

```
import azure.functions as func
import azurefunctions.extensions.bindings.blob as blob
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.blob_trigger(
arg_name="client", path="PATH/TO/BLOB", connection="AzureWebJobsStorage"
)
def blob_trigger(client: blob.BlobClient):
logging.info(
f"Python blob trigger function processed blob \n"
f"Properties: {client.get_blob_properties()}\n"
f"Blob content head: {client.download_blob().read(size=1)}"
)
```


For examples of using other SDK types, see the [ ContainerClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_storagestreamdownloader/function_app.py)

`StorageStreamDownloader`

[Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

This example logs information from the incoming blob metadata.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobTrigger1")
@app.blob_trigger(arg_name="myblob",
path="PATH/TO/BLOB",
connection="CONNECTION_SETTING")
def test_function(myblob: func.InputStream):
logging.info(f"Python blob trigger function processed blob \n"
f"Name: {myblob.name}\n"
f"Blob Size: {myblob.length} bytes")
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [BlobAttribute](/en-us/dotnet/api/microsoft.azure.webjobs.blobattribute) attribute to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-trigger).

The attribute's constructor takes the following parameters:

| Parameter | Description |
|---|---|
BlobPath |
The path to the blob. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

**Access****Source**`BlobTriggerSource.EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`BlobTriggerSource.LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.Here's an `BlobTrigger`

attribute in a method signature:

```
[Function(nameof(BlobFunction))]
[BlobOutput("test-samples-output/{name}-output.txt")]
public static string Run(
[BlobTrigger("test-samples-trigger/{name}")] string myTriggerItem,
[BlobInput("test-samples-input/sample1.txt")] string myBlob,
FunctionContext context)
```


When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using decorators, the following properties on the `blob_trigger`

decorator define the Blob Storage trigger:

| Property | Description |
|---|---|
`arg_name` |
Declares the parameter name in the function signature. When the function is triggered, this parameter's value has the contents of the queue message. |
`path` |
The
|

`connection`

`source`

`EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobTrigger`

attribute is used to give you access to the blob that triggered the function. Refer to the [trigger example](#example) for details. Use the `source`

property to set the source of the triggering event. Use `EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is `LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container. |

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The
|

**connection**[Connections](#connections).**source**`EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `blobTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. |
path |
The
|

**connection**[Connections](#connections).**source**`EventGrid`

for an [Event Grid-based blob trigger](functions-event-grid-blob-trigger), which provides lower latency. The default is`LogsAndContainerScan`

, which uses the standard polling mechanism to detect changes in the container.See the [Example section](#example) for complete examples.

## Metadata

The blob trigger provides several metadata properties. These properties can be used as part of binding expressions in other bindings or as parameters in your code. These values have the same semantics as the [CloudBlob](/en-us/dotnet/api/microsoft.azure.storage.blob.cloudblob) type.

| Property | Type | Description |
|---|---|---|
`BlobTrigger` |
`string` |
The path to the triggering blob. |
`Uri` |
`System.Uri` |
The blob's URI for the primary location. |
`Properties` |
|

`Metadata`

`IDictionary<string,string>`

The following example logs the path to the triggering blob, including the container:

```
public static void Run(string myBlob, string blobTrigger, ILogger log)
{
log.LogInformation($"Full blob path: {blobTrigger}");
}
```


## Metadata

The blob trigger provides several metadata properties. These properties can be used as part of binding expressions in other bindings or as parameters in your code.

| Property | Description |
|---|---|
`blobTrigger` |
The path to the triggering blob. |
`uri` |
The blob's URI for the primary location. |
`properties` |
The blob's system properties. |
`metadata` |
The user-defined metadata for the blob. |

## Metadata

Metadata is available through the `$TriggerMetadata`

parameter.

## Usage

The binding types supported by Blob trigger depend on the extension package version and the C# modality used in your function app.

The blob trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small. This is recommended because the entire blob contents are loaded into memory. For most blobs, use a `Stream`

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

Note

Support for binding to SDK types is currently in preview and limited to the Azure Blob Storage SDK. For more information, see [SDK types](functions-reference-java#sdk-types) in the Java reference article.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

Access blob data via the parameter typed as [InputStream](/en-us/python/api/azure-functions/azure.functions.inputstream). Refer to the [trigger example](#example) for details.

Functions also support Python SDK type bindings for Azure Blob storage, which lets you work with blob data using these underlying SDK types:

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

## Blob name patterns

You can specify a blob name pattern in the `path`

property in *function.json* or in the `BlobTrigger`

attribute constructor. The name pattern can be a [filter or binding expression](functions-bindings-expressions-patterns). The following sections provide examples.

Tip

A container name can't contain a resolver in the name pattern.

### Get file name and extension

The following example shows how to bind to the blob file name and extension separately:

```
"path": "input/{blobname}.{blobextension}",
```


If the blob is named *original-Blob1.txt*, the values of the `blobname`

and `blobextension`

variables in function code are *original-Blob1* and *txt*.

### Filter on blob name

The following example triggers only on blobs in the `input`

container that start with the string "original-":

```
"path": "input/original-{name}",
```


If the blob name is *original-Blob1.txt*, the value of the `name`

variable in function code is `Blob1.txt`

.

### Filter on file type

The following example triggers only on *.png* files:

```
"path": "samples/{name}.png",
```


### Filter on curly braces in file names

To look for curly braces in file names, escape the braces by using two braces. The following example filters for blobs that have curly braces in the name:

```
"path": "images/{{20140101}}-{name}",
```


If the blob is named *{20140101}-soundfile.mp3*, the `name`

variable value in the function code is *soundfile.mp3*.

## Polling and latency

Polling works as a hybrid between inspecting logs and running periodic container scans. Blobs are scanned in groups of 10,000 at a time with a continuation token used between intervals. If your function app is on the Consumption plan, there can be up to a 10-minute delay in processing new blobs if a function app has gone idle.

Warning

[Storage logs are created on a "best effort"](/en-us/rest/api/storageservices/About-Storage-Analytics-Logging) basis. There's no guarantee that all events are captured. Under some conditions, logs may be missed.

If you require faster or more reliable blob processing, you should consider switching your hosting to use an App Service plan with Always On enabled, which may result in increased costs. You might also consider using a trigger other than the classic polling blob trigger. For more information and a comparison of the various triggering options for blob storage containers, see [Trigger on a blob container](storage-considerations#trigger-on-a-blob-container).

## Blob receipts

The Azure Functions runtime ensures that no blob trigger function gets called more than once for the same new or updated blob. To determine if a given blob version has been processed, it maintains *blob receipts*.

Azure Functions stores blob receipts in a container named *azure-webjobs-hosts* in the Azure storage account for your function app (defined by the app setting `AzureWebJobsStorage`

). A blob receipt has the following information:

- The triggered function (
`<FUNCTION_APP_NAME>.Functions.<FUNCTION_NAME>`

, for example:`MyFunctionApp.Functions.CopyBlob`

) - The container name
- The blob type (
`BlockBlob`

or`PageBlob`

) - The blob name
- The ETag (a blob version identifier, for example:
`0x8D1DC6E70A277EF`

)

To force reprocessing of a blob, delete the blob receipt for that blob from the *azure-webjobs-hosts* container manually. While reprocessing might not occur immediately, it's guaranteed to occur at a later point in time. To reprocess immediately, the *scaninfo* blob in *azure-webjobs-hosts/blobscaninfo* can be updated. Any blobs with a last modified timestamp after the `LatestScan`

property will be scanned again.

## Poison blobs

When a blob trigger function fails for a given blob, Azure Functions retries that function a total of five times by default.

If all five tries fail, Azure Functions adds a message to a Storage queue named *webjobs-blobtrigger-poison*. The maximum number of retries is configurable. The same MaxDequeueCount setting is used for poison blob handling and poison queue message handling. The queue message for poison blobs is a JSON object that contains the following properties:

- FunctionId (in the format
`<FUNCTION_APP_NAME>.Functions.<FUNCTION_NAME>`

) - BlobType (
`BlockBlob`

or`PageBlob`

) - ContainerName
- BlobName
- ETag (a blob version identifier, for example:
`0x8D1DC6E70A277EF`

)

## Memory usage and concurrency

When you bind to an [output type](#usage) that doesn't support streaming, such as `string`

, or `Byte[]`

, the runtime must load the entire blob into memory more than one time during processing. This can result in higher-than expected memory usage when processing blobs. When possible, use a stream-supporting type. Type support depends on the C# mode and extension version. For more information, see [Binding types](functions-bindings-storage-blob#binding-types).

At this time, the runtime must load the entire blob into memory more than one time during processing. This can result in higher-than expected memory usage when processing blobs.

Memory usage can be further impacted when multiple function instances are concurrently processing blob data. If you are having memory issues using a Blob trigger, consider reducing the number of concurrent executions permitted. Reducing the concurrency can have the side effect of increasing the backlog of blobs waiting to be processed. The memory limits of your function app depend on the plan. For more information, see [Service limits](functions-scale#service-limits).

The way that you can control the number of concurrent executions depends on the version of the Storage extension you are using.

When using version 5.0.0 of the Storage extension or a later version, you control trigger concurrency by using the `maxDegreeOfParallelism`

setting in the [blobs configuration in host.json](functions-bindings-storage-blob#hostjson-settings).

Limits apply separately to each function that uses a blob trigger.

## host.json properties

The [host.json](functions-host-json#blobs) file contains settings that control blob trigger behavior. See the [host.json settings](functions-bindings-storage-blob#hostjson-settings) section for details regarding available settings.
