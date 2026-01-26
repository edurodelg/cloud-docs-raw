---
merged_at: 2026-01-26T23:29:57.706660
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-output -->

# Apache Kafka output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The output binding enables an Azure Functions app to send messages to a Kafka topic.

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

How you use the binding depends on the C# modality in your function app. You can use one of the following modalities:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example uses a custom return type named `MultipleOutputType`

, which consists of an HTTP response and a Kafka output.

```
[Function("KafkaOutput")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = message,
HttpResponse = response
};
}
```


In the `MultipleOutputType`

class, `Kevent`

is the output binding variable for the Kafka binding.

```
public class MultipleOutputType
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string Kevent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


To send a batch of events, pass a string array to the output type, as shown in the following example:

```
[Function("KafkaOutputMany")]
public static MultipleOutputTypeForBatch Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
var response = req.CreateResponse(HttpStatusCode.OK);
string[] messages = new string[2];
messages[0] = "one";
messages[1] = "two";
return new MultipleOutputTypeForBatch()
{
Kevents = messages,
HttpResponse = response
};
}
```


The string array is defined as the `Kevents`

property on the class, and the output binding is defined on this property:

```
public class MultipleOutputTypeForBatch
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string[] Kevents { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following function adds headers to the Kafka output data:

```
[Function("KafkaOutputWithHeaders")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
string kevent = "{ \"Offset\":364,\"Partition\":0,\"Topic\":\"kafkaeventhubtest1\",\"Timestamp\":\"2022-04-09T03:20:06.591Z\", \"Value\": \"" + message + "\", \"Headers\": [{ \"Key\": \"test\", \"Value\": \"dotnet-isolated\" }] }";
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = kevent,
HttpResponse = response
};
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/confluent).

The usage of the output binding depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your output binding directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
const { app, output } = require("@azure/functions");
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
async function kafkaOutputManyWithHttp(request, context) {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "javascript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputManyWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "typescript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the function.json file depend on your event provider, which in these examples are either Confluent or Azure Event Hubs. The following examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

The following function.json defines the trigger for the specific provider in these examples:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get"
]
},
{
"type": "kafka",
"name": "outputMessage",
"brokerList": "BrokerList",
"topic": "topic",
"username" : "%ConfluentCloudUserName%",
"password" : "%ConfluentCloudPassword%",
"protocol": "SASLSSL",
"authenticationMode": "PLAIN",
"direction": "out"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


The following code sends a message to the topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
$message
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following code sends multiple messages as an array to the same topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
$message = @("one", "two")
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following example shows how to send an event message with headers to the same Kafka topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
if (-not $message) {
$message = $Request.Body.Message
}
$kevent = @{
Offset = 364
Partition = 0
Topic = "kafkaeventhubtest1"
Timestamp = "2022-04-09T03:20:06.591Z"
Value = $message
Headers= @(@{
Key= "test"
Value= "powershell"
}
)
}
Push-OutputBinding -Name Message -Value $kevent
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = 'ok'
})
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the output binding depends on your version of the Python programming model.

In the Python v2 model, you define your output binding directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
input_msg = req.params.get('message')
outputMessage.set(input_msg)
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputMany")
@KafkaOutput.route(route="kafka_output_many")
@KafkaOutput.kafka_output(arg_name="outputMessage", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain", data_type="string")
def kafka_output_many(req: func.HttpRequest, outputMessage: func.Out[str] ) -> func.HttpResponse:
outputMessage.set(json.dumps(['one', 'two']))
return 'OK'
```


To send events in a batch, send an array of messages, as shown in these examples:

```
@KafkaOutput.route(route="kafka_output_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
kevent = { "Offset":0,"Partition":0,"Topic":"dummy","Timestamp":"2022-04-09T03:20:06.591Z", "Value": message, "Headers": [{ "Key": "test", "Value": "python" }] }
out.set(json.dumps(kevent))
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputManyWithHeaders")
@KafkaOutput.route(route="kafka_output_many_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_many_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
kevent = [{ "Offset": 364, "Partition":0,"Topic":"kafkaeventhubtest1","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "one", "Headers": [{ "Key": "test", "Value": "python" }] },
```


These examples show how to send an event message with headers to a Kafka topic:

For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure the output binding depend on the specific event provider.

The following function sends a message to the Kafka topic.

```
@FunctionName("KafkaOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
context.getLogger().info("Message:" + message);
output.setValue(message);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
```


The following example shows how to send multiple messages to a Kafka topic.

```
@FunctionName("KafkaOutputMany")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String[]> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String[] messages = new String[2];
messages[0] = "one";
messages[1] = "two";
output.setValue(messages);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


In this example, the output binding parameter is changed to string array.

The last example uses these `KafkaEntity`

and `KafkaHeader`

classes:

```
public class KafkaEntity {
public int Offset;
public int Partition;
public String Timestamp;
public String Topic;
public String Value;
public KafkaHeaders Headers[];
public KafkaEntity(int Offset, int Partition, String Topic, String Timestamp, String Value,KafkaHeaders[] headers) {
this.Offset = Offset;
this.Partition = Partition;
this.Topic = Topic;
this.Timestamp = Timestamp;
this.Value = Value;
this.Headers = headers;
}
```


```
public class KafkaHeaders{
public String Key;
public String Value;
public KafkaHeaders(String key, String value) {
this.Key = key;
this.Value = value;
}
```


The following example function sends a message with headers to a Kafka topic.

```
@FunctionName("KafkaOutputWithHeaders")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<KafkaEntity> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
KafkaHeaders[] headers = new KafkaHeaders[1];
headers[0] = new KafkaHeaders("test", "java");
KafkaEntity kevent = new KafkaEntity(364, 0, "topic", "2022-04-09T03:20:06.591Z", message, headers);
output.setValue(kevent);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `Kafka`

attribute to define the function trigger.

The following table explains the properties you can set by using this attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**Topic****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**MaxMessageBytes**`1`

.**BatchSize**`10000`

.**EnableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

**MessageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**RequestTimeoutMs**`5000`

.**MaxRetries**`2`

. Retrying may cause reordering, unless `EnableIdempotence`

is set to `true`

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

The `KafkaOutput`

annotation enables you to create a function that writes to a specific topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**avroSchema**[Currently not supported for Java](https://github.com/Azure/azure-functions-java-library/issues/198).)**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

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

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

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

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

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
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authentication_mode**`NOTSET`

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

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The offset, partition, and timestamp for the event are generated at runtime. You can set only the value and headers inside the function. You set the topic in the function.json file.

Make sure you have access to the Kafka topic where you want to write. You configure the binding with access and connection credentials to the Kafka topic.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer-input -->

# Azure Data Explorer input bindings for Azure Functions (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Data Explorer input binding retrieves data from a database.

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Data Explorer input binding (out of process) are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to a `Product`

class and the Products table, both of which are defined in the previous sections.

### HTTP trigger, get row by ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single record. The function is triggered by an HTTP request that uses a query string to specify the ID. That ID is used to retrieve a `Product`

record with the specified query.

Note

The HTTP query string parameter is case sensitive.

```
using System.Text.Json.Nodes;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.InputBindingSamples
{
public static class GetProductsQuery
{
[Function("GetProductsQuery")]
public static JsonArray Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproductsquery")] HttpRequestData req,
[KustoInput(Database: "productsdb",
KqlCommand = "declare query_parameters (productId:long);Products | where ProductID == productId",
KqlParameters = "@productId={Query.productId}",Connection = "KustoConnectionString")] JsonArray products)
{
return products;
}
}
}
```


### HTTP trigger, get multiple rows from route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves records returned by the query (based on the name of the product, in this case). The function is triggered by an HTTP request that uses route data to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.InputBindingSamples
{
public static class GetProductsFunction
{
[Function("GetProductsFunction")]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproductsfn/{name}")] HttpRequestData req,
[KustoInput(Database: "productsdb",
KqlCommand = "declare query_parameters (name:string);GetProductsByName(name)",
KqlParameters = "@name={name}",Connection = "KustoConnectionString")] IEnumerable<Product> products)
{
return products;
}
}
}
```


More samples for the Java Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `Product`

class (in a separate file `Product.java`

) and a corresponding database table.

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("Name")
public String Name;
@JsonProperty("Cost")
public double Cost;
public Product() {
}
public Product(long ProductID, String name, double Cost) {
this.ProductID = ProductID;
this.Name = name;
this.Cost = Cost;
}
}
```


### HTTP trigger, get multiple rows

The example uses a route parameter to specify the name of the ID of the products. All matching products are retrieved from the products table.

```
package com.microsoft.azure.kusto.inputbindings;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoInput;
import com.microsoft.azure.kusto.common.Product;
import java.util.Optional;
public class GetProducts {
@FunctionName("GetProducts")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {
HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "getproducts/{productId}") HttpRequestMessage<Optional<String>> request,
@KustoInput(name = "getjproducts", kqlCommand = "declare query_parameters (productId:long);Products | where ProductID == productId",
kqlParameters = "@productId={productId}", database = "productsdb", connection = "KustoConnectionString") Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products)
.build();
}
}
```


### HTTP trigger, get row by ID from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
package com.microsoft.azure.kusto.inputbindings;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoInput;
import com.microsoft.azure.kusto.common.Product;
import java.util.Optional;
public class GetProductsQueryString {
@FunctionName("GetProductsQueryString")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "getproducts") HttpRequestMessage<Optional<String>> request,
@KustoInput(name = "getjproductsquery", kqlCommand = "declare query_parameters (name:string);GetProductsByName(name)",
kqlParameters = "@name={Query.name}", database = "productsdb", connection = "KustoConnectionString") Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products)
.build();
}
}
```


More samples for the Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node).

This section contains the following examples:

The examples refer to a database table:

### HTTP trigger, get multiple rows

The following example shows an Azure Data Explorer input binding in a *function.json* file and a JavaScript function that reads from a query and returns the results in the HTTP response.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproducts/{productId}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (productId:long);Products | where ProductID == productId",
"kqlParameters": "@productId={productId}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req, productget) {
return {
status: 200,
body: productget
};
}
```


### HTTP trigger, get row by name from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproductsfn"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productfnget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (name:string);GetProductsByName(name)",
"kqlParameters": "@name={Query.name}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req, producproductfngettget) {
return {
status: 200,
body: productfnget
};
}
```


More samples for the Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python).

This section contains the following examples:

### HTTP trigger, get multiple rows

The following example shows an Azure Data Explorer input binding in a *function.json* file and a Python function that reads from a query and returns the results in the HTTP response.

The following binding data is in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
],
"route": "getproducts/{productId}"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "productsdb",
"type": "kusto",
"database": "sdktestsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (productId:long);Products | where ProductID == productId",
"kqlParameters": "@productId={Query.productId}",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, products: str) -> func.HttpResponse:
return func.HttpResponse(
products,
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get row by ID from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproductsfn"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productfnget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (name:string);GetProductsByName(name)",
"kqlParameters": "@name={Query.name}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
def main(req: func.HttpRequest, products: str) -> func.HttpResponse:
return func.HttpResponse(
products,
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [KustoAttribute](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/src/KustoAttribute.cs) attribute to declare the Azure Data Explorer bindings on the function, which has the following properties.

| Attribute property | Description |
|---|---|
| Database | Required. The database against which the query must be executed. |
| Connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| KqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| KqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| ManagedServiceIdentity | Optional. You can use a managed identity to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

## Annotations

The [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) uses the [ @KustoInput](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/java-library/src/main/java/com/microsoft/azure/functions/kusto/annotation/KustoInput.java) annotation (

`com.microsoft.azure.functions.kusto.annotation.KustoInput`

).| Element | Description |
|---|---|
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| kqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| kqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| managedServiceIdentity | A managed identity can be used to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
| type | Required. Must be set to `kusto` . |
| direction | Required. Must be set to `in` . |
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| kqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| kqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| managedServiceIdentity | A managed identity can be used to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the database and the attributes `KQLCommand`

and `KQLParameters`

and the connection setting name. The KQL command can be a KQL statement or a KQL function. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For example: `"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId`

. Queries executed by the input binding are parameterized. The values provided in the KQL parameters are used at runtime.

Important

For optimal security, your function app should use managed identities when connecting to Azure Data Explorer instead of using a connection string, which contains keys. For more information, see [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For mananaged identity-based connections, you must set the `managedServiceIdentity`

property in the binding definition.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-textcompletion-input -->

# Azure OpenAI text completion input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI text completion input binding allows you to bring the results text completion APIs into your code executions. You can define the binding to use both predefined prompts with parameters or pass through an entire prompt.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI completions, see [Learn how to generate or manipulate text](/en-us/azure/ai-services/openai/how-to/completions).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
[Function(nameof(WhoIs))]
public static IActionResult WhoIs(
[HttpTrigger(AuthorizationLevel.Function, Route = "whois/{name}")] HttpRequestData req,
[TextCompletionInput("Who is {name}?", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%")] TextCompletionResponse response)
{
return new OkObjectResult(response.Content);
}
```


This example takes a prompt as input, sends it directly to the completions API, and returns the response as the output.

```
[Function(nameof(GenericCompletion))]
public static IActionResult GenericCompletion(
[HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequestData req,
[TextCompletionInput("{Prompt}", ChatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%")] TextCompletionResponse response,
ILogger log)
{
string text = response.Content;
return new OkObjectResult(text);
}
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
@FunctionName("WhoIs")
public HttpResponseMessage whoIs(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "whois/{name}")
HttpRequestMessage<Optional<String>> request,
@BindingName("name") String name,
@TextCompletion(prompt = "Who is {name}?", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", name = "response", isReasoningModel = false) TextCompletionResponse response,
final ExecutionContext context) {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response.getContent())
.build();
}
```


This example takes a prompt as input, sends it directly to the completions API, and returns the response as the output.

```
@FunctionName("GenericCompletion")
public HttpResponseMessage genericCompletion(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@TextCompletion(prompt = "{prompt}", chatModel = "%CHAT_MODEL_DEPLOYMENT_NAME%", name = "response", isReasoningModel = false) TextCompletionResponse response,
final ExecutionContext context) {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(response.getContent())
.build();
}
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
const { app, input } = require("@azure/functions");
// This OpenAI completion input requires a {name} binding value.
const openAICompletionInput = input.generic({
prompt: 'Who is {name}?',
maxTokens: '100',
type: 'textCompletion',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%'
})
app.http('whois', {
methods: ['GET'],
route: 'whois/{name}',
authLevel: 'function',
extraInputs: [openAICompletionInput],
handler: async (_request, context) => {
var response = context.extraInputs.get(openAICompletionInput)
return { body: response.content.trim() }
}
});
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
import { app, input } from "@azure/functions";
// This OpenAI completion input requires a {name} binding value.
const openAICompletionInput = input.generic({
prompt: 'Who is {name}?',
maxTokens: '100',
type: 'textCompletion',
chatModel: '%CHAT_MODEL_DEPLOYMENT_NAME%'
})
app.http('whois', {
methods: ['GET'],
route: 'whois/{name}',
authLevel: 'function',
extraInputs: [openAICompletionInput],
handler: async (_request, context) => {
var response: any = context.extraInputs.get(openAICompletionInput)
return { body: response.content.trim() }
}
});
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for `TextCompletionResponse`

:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "whois/{name}",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "textCompletion",
"direction": "in",
"name": "TextCompletionResponse",
"prompt": "Who is {name}?",
"maxTokens": "100",
"chatModel": "%CHAT_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

The code simply returns the text from the completion API as the response:

```
using namespace System.Net
param($Request, $TriggerMetadata, $TextCompletionResponse)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $TextCompletionResponse.Content
})
```


This example demonstrates the *templating* pattern, where the HTTP trigger function takes a `name`

parameter and embeds it into a text prompt, which is then sent to the Azure OpenAI completions API by the extension. The response to the prompt is returned in the HTTP response.

```
@app.route(route="whois/{name}", methods=["GET"])
@app.text_completion_input(
arg_name="response",
prompt="Who is {name}?",
max_tokens="100",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
)
def whois(req: func.HttpRequest, response: str) -> func.HttpResponse:
response_json = json.loads(response)
return func.HttpResponse(response_json["content"], status_code=200)
```


This example takes a prompt as input, sends it directly to the completions API, and returns the response as the output.

```
@app.route(route="genericcompletion", methods=["POST"])
@app.text_completion_input(
arg_name="response",
prompt="{Prompt}",
chat_model="%CHAT_MODEL_DEPLOYMENT_NAME%",
)
def genericcompletion(
req: func.HttpRequest,
response: str
) -> func.HttpResponse:
response_json = json.loads(response)
return func.HttpResponse(response_json["content"], status_code=200)
```


## Attributes

The specific attribute you apply to define a text completion input binding depends on your C# process mode.

In the [isolated worker model](dotnet-isolated-process-guide), apply `TextCompletionInput`

to define a text completion input binding.

The attribute supports these parameters:

| Parameter | Description |
|---|---|
Prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
ChatModel |
Optional. Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
Temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
TopP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
MaxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
IsReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Annotations

The `TextCompletion`

annotation enables you to define a text completion input binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Decorators

During the preview, define the input binding as a `generic_input_binding`

binding of type `textCompletion`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chat_model |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
top_p |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
max_tokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
is_reasoning _model |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `textCompletion` . |
direction |
Must be `in` . |
name |
The name of the input binding. |
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
prompt |
Gets or sets the prompt to generate completions for, encoded as a string. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
chatModel |
Gets or sets the ID of the model to use as a string, with a default value of `gpt-3.5-turbo` . |
temperature |
Optional. Gets or sets the sampling temperature to use, as a string between `0` and `2` . Higher values (`0.8` ) make the output more random, while lower values like (`0.2` ) make output more focused and deterministic. You should use either `Temperature` or `TopP` , but not both. |
topP |
Optional. Gets or sets an alternative to sampling with temperature, called nucleus sampling, as a string. In this sampling method, the model considers the results of the tokens with `top_p` probability mass. So `0.1` means only the tokens comprising the top 10% probability mass are considered. You should use either `Temperature` or `TopP` , but not both. |
maxTokens |
Optional. Gets or sets the maximum number of tokens to generate in the completion, as a string with a default of `100` . The token count of your prompt plus `max_tokens` can't exceed the model's context length. Most models have a context length of 2,048 tokens (except for the newest models, which support 4096). |
isReasoningModel |
Optional. Gets or sets a value indicating whether the chat completion model is a reasoning model. This option is experimental and associated with the reasoning model until all models have parity in the expected properties, with a default value of `false` . |

## Usage

See the [Example section](#example) for complete examples.
