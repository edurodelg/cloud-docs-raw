---
merged_at: 2026-01-29T15:49:53.287128
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-cosmos-db-vs-code -->

# Connect Azure Functions to Azure Cosmos DB using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

This article shows you how to use Visual Studio Code to connect [Azure Cosmos DB](/en-us/azure/cosmos-db/introduction) to the function you created in the previous quickstart article. The output binding that you add to this function writes data from the HTTP request to a JSON document stored in an Azure Cosmos DB container.

Before you begin, you must complete the [quickstart: Create a C# function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the [quickstart: Create a JavaScript function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript?pivot=nodejs-model-v3). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Note

This article currently only supports [Node.js v3 for Functions](functions-reference-node?pivots=nodejs-model-v3).

Before you begin, you must complete the [quickstart: Create a Python function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

## Configure your environment

Before you get started, make sure to install the [Azure Databases extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb) for Visual Studio Code.

## Create your Azure Cosmos DB account

Now, you create an Azure Cosmos DB account as a [serverless account type](/en-us/azure/cosmos-db/serverless). This consumption-based mode makes Azure Cosmos DB a strong option for serverless workloads.

In Visual Studio Code, select

**View**>**Command Palette...**then in the command palette search for`Azure Databases: Create Server...`

Provide the following information at the prompts:

Prompt Selection **Select an Azure Database Server**Choose **Core (NoSQL)**to create a document database that you can query by using a SQL syntax or a Query Copilot ([Preview](/en-us/azure/cosmos-db/nosql/query/how-to-enable-use-copilot)) converting natural language prompts to queries.[Learn more about the Azure Cosmos DB](/en-us/azure/cosmos-db/introduction).**Account name**Enter a unique name to identify your Azure Cosmos DB account. The account name can use only lowercase letters, numbers, and hyphens (-), and must be between 3 and 31 characters long. **Select a capacity model**Select **Serverless**to create an account in[serverless](/en-us/azure/cosmos-db/serverless)mode.**Select a resource group for new resources**Choose the resource group where you created your function app in the [previous article](how-to-create-function-vs-code?pivot=programming-language-csharp).**Select a location for new resources**Select a geographic location to host your Azure Cosmos DB account. Use the location that's closest to you or your users to get the fastest access to your data. After your new account is provisioned, a message is displayed in notification area.


## Create an Azure Cosmos DB database and container

Select the Azure icon in the Activity bar, expand

**Resources**>**Azure Cosmos DB**, right-click (Ctrl+select on macOS) your account, and select**Create database...**.Provide the following information at the prompts:

Prompt Selection **Database name**Type `my-database`

.**Enter and ID for your collection**Type `my-container`

.**Enter the partition key for the collection**Type `/id`

as the[partition key](/en-us/azure/cosmos-db/partitioning-overview).Select

**OK**to create the container and database.

## Update your function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure. In this article, you update your app to write JSON documents to the Azure Cosmos DB container you've created. To connect to your Azure Cosmos DB account, you must add its connection string to your app settings. You then download the new setting to your local.settings.json file so you can connect to your Azure Cosmos DB account when running locally.

In Visual Studio Code, right-click (Ctrl+select on macOS) on your new Azure Cosmos DB account, and select

**Copy Connection String**.Press

`F1`to open the command palette, then search for and run the command`Azure Functions: Add New Setting...`

.Choose the function app you created in the previous article. Provide the following information at the prompts:

Prompt Selection **Enter new app setting name**Type `CosmosDbConnectionString`

.**Enter value for "CosmosDbConnectionString"**Paste the connection string of your Azure Cosmos DB account you copied. You can also configure [Microsoft Entra identity](functions-bindings-cosmosdb-v2-trigger#connections)as an alternative.This creates an application setting named connection

`CosmosDbConnectionString`

in your function app in Azure. Now, you can download this setting to your local.settings.json file.Press

`F1`again to open the command palette, then search for and run the command`Azure Functions: Download Remote Settings...`

.Choose the function app you created in the previous article. Select

**Yes to all**to overwrite the existing local settings.

This downloads all of the setting from Azure to your local project, including the new connection string setting. Most of the downloaded settings aren't used when running locally.

## Register binding extensions

Because you're using an Azure Cosmos DB output binding, you must have the corresponding bindings extension installed before you run the project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Azure Cosmos DB extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.CosmosDB
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway"
}
}
}
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


Now, you can add the Azure Cosmos DB output binding to your project.

## Add an output binding

In a C# class library project, the bindings are defined as binding attributes on the function method.

Open the *HttpExample.cs* project file and add the following classes:

```
public class MultiResponse
{
[CosmosDBOutput("my-database", "my-container",
Connection = "CosmosDbConnectionSetting", CreateIfNotExists = true)]
public MyDocument Document { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
public class MyDocument {
public string id { get; set; }
public string message { get; set; }
}
```


The `MyDocument`

class defines an object that gets written to the database. The connection string for the Storage account is set by the `Connection`

property. In this case, you could omit `Connection`

because you're already using the default storage account.

The `MultiResponse`

class allows you to both write to the specified collection in the Azure Cosmos DB and return an HTTP success message. Because you need to return a `MultiResponse`

object, you need to also update the method signature.

Specific attributes specify the name of the container and the name of its parent database. The connection string for your Azure Cosmos DB account is set by the `CosmosDbConnectionString`

.

Binding attributes are defined directly in your function code. The [Azure Cosmos DB output configuration](functions-bindings-cosmosdb-v2-output#configuration) describes the fields required for an Azure Cosmos DB output binding.

For this `MultiResponse`

scenario, you need to add an `extraOutputs`

output binding to the function.

```
app.http('HttpExample', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
```


Add the following properties to the binding configuration:

```
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
```


Binding attributes are defined directly in the *function_app.py* file. You use the `cosmos_db_output`

decorator to add an [Azure Cosmos DB output binding](functions-bindings-triggers-python#azure-cosmos-db-output-binding):

```
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database",
container_name="my-container", connection="CosmosDbConnectionString")
```


In this code, `arg_name`

identifies the binding parameter referenced in your code, `database_name`

and `container_name`

are the database and collection names that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Azure Cosmos DB account, which is in the `CosmosDbConnectionString`

setting in the *local.settings.json* file.

## Add code that uses the output binding

Replace the existing Run method with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and Azure Cosmos DB output binding.
return new MultiResponse()
{
Document = new MyDocument
{
id = System.Guid.NewGuid().ToString(),
message = message
},
HttpResponse = response
};
}
```


Add code that uses the `extraInputs`

output binding object on `context`

to send a JSON document to the named output binding function, `sendToCosmosDb`

. Add this code before the `return`

statement.

```
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
```


At this point, your function should look as follows:

```
const { app, output } = require('@azure/functions');
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
app.http('HttpExampleToCosmosDB', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
if (!name) {
return { status: 404, body: 'Missing required data' };
}
// Output to Database
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
const responseMessage = name
? 'Hello, ' +
name +
'. This HTTP triggered function executed successfully.'
: 'This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.';
// Return to HTTP client
return { body: responseMessage };
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


This code now returns a `MultiResponse`

object that contains both a document and an HTTP response.

Update *HttpExample\function_app.py* to match the following code. Add the `outputDocument`

parameter to the function definition and `outputDocument.set()`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.FUNCTION)
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database", container_name="my-container", connection="CosmosDbConnectionString")
def test_function(req: func.HttpRequest, msg: func.Out[func.QueueMessage],
outputDocument: func.Out[func.Document]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
logging.info('Python Cosmos DB trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
outputDocument.set(func.Document.from_dict({"id": name}))
msg.set(name)
return func.HttpResponse(f"Hello {name}!")
else:
return func.HttpResponse(
"Please pass a name on the query string or in the request body",
status_code=400
)
```


The document `{"id": "name"}`

is created in the database collection specified in the binding.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure. If you don't already have Core Tools installed locally, you are prompted to install it the first time you run your project.

To call your function, press

`F5`to start the function app project. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you don't already have Core Tools installed, select

**Install**to install Core Tools when prompted to do so.

If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to**WSL Bash**.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the`HttpExample`

function and choose**Execute Function Now...**.In the

**Enter request body**, press`Enter`to send a request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in the

**Terminal**panel.Press

`Ctrl + C`to stop Core Tools and disconnect the debugger.

## Run the function locally

As in the previous article, press

`F5`to start the function app project and Core Tools.With Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Ctrl-click on Mac) the`HttpExample`

function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.After a response is returned, press

`Ctrl + C`to stop Core Tools.

### Verify that a JSON document has been created

On the Azure portal, go back to your Azure Cosmos DB account and select

**Data Explorer**.Expand your database and container, and select

**Items**to list the documents created in your container.Verify that a new JSON document has been created by the output binding.


## Redeploy and verify the updated app

In Visual Studio Code, press F1 to open the command palette. In the command palette, search for and select

`Azure Functions: Deploy to function app...`

.Choose the function app that you created in the first article. Because you're redeploying your project to the same app, select

**Deploy**to dismiss the warning about overwriting files.After deployment completes, you can again use the

**Execute Function Now...**feature to trigger the function in Azure. This command automatically retrieves the function access key and uses it when calling the HTTP trigger endpoint.Again

[check the documents created in your Azure Cosmos DB container](#verify-that-a-json-document-has-been-created)to verify that the output binding again generates a new JSON document.

## Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write JSON documents to an Azure Cosmos DB container. Now you can learn more about developing Functions using Visual Studio Code:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan -->

# Azure Functions Flex Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Flex Consumption is a Linux-based Azure Functions hosting plan that builds on the Consumption *pay for what you use* serverless billing model. It gives you more flexibility and customizability by introducing private networking, instance memory size selection, and fast/large scale-out features still based on a *serverless* model.

You can review end-to-end samples that feature the Flex Consumption plan in the [Flex Consumption plan samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples).

## Benefits

The Flex Consumption plan builds on the strengths of the serverless Consumption plan, which include dynamic scaling and execution-based billing. With Flex Consumption, you also get these extra features:

**Reduced Cold Start Times**: Enable[always-ready instances](#always-ready-instances)to achieve faster cold-start times compared to the Consumption plan.**Virtual network support**:[Virtual network integration](#virtual-network-integration)enables your serverless app to run in a virtual network.**Per-Function Scaling**: Each function in your app[scales independently based on its workload](#per-function-scaling), potentially resulting in more efficient resource allocation.**Improved Concurrency Handling**: Better handling of concurrent executions with configurable concurrency settings per function.**Flexible Memory Configuration**: Flex Consumption offers multiple[instance sizes](#instance-sizes)size options, allowing you to optimize for your specific workload requirements.

This table helps you directly compare the features of Flex Consumption with the Consumption hosting plan:

| Feature | Consumption | Flex Consumption |
|---|---|---|
| Scale to zero | ✅ Yes | ✅ Yes |
| Scale behavior |
|

[Event driven](event-driven-scaling)(fast)For a complete comparison of the Flex Consumption plan against the Consumption plan and all other plan and hosting types, see [function scale and hosting options](functions-scale).

Tip

If you're migrating from the Linux Consumption plan, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux) for step-by-step migration instructions and important differences between the plans.

## Virtual network integration

Flex Consumption expands on the traditional benefits of Consumption plan by adding support for [virtual network integration](functions-networking-options#virtual-network-integration). When your apps run in a Flex Consumption plan, they can connect to other Azure services secured inside a virtual network. All while still allowing you to take advantage of serverless billing and scale, together with the scale and throughput benefits of the Flex Consumption plan. For more information, see [Enable virtual network integration](flex-consumption-how-to#enable-virtual-network-integration).

## Instance sizes

When you create your function app in a Flex Consumption plan, you can select the memory size of the instances on which your app runs. See [Billing](#billing) to learn how instance memory sizes affect the costs of your function app.

Currently, Flex Consumption offers these instance size options:

| Instance Memory (MB) | CPU Cores |
|---|---|
| 512 | 0.25 |
| 2048 | 1 |
| 4096 | 2 |

Note

The CPU core values shown are typical allocations for instances with the specified memory size. However, initial instances might be granted slightly different core allocations to improve performance. Each Flex Consumption instance also includes an extra 272 MB of memory allocated by the platform as a buffer for system and host processes. This extra memory doesn't affect billing, and instances are billed based on the configured instance memory size shown in the preceding table.

When deciding on which instance memory size to use with your apps, here are some things to consider:

- The 2,048-MB instance memory size is the default and should be used for most scenarios. The 512 MB and 4,096-MB instance memory sizes are available for scenarios that best suit your application's concurrency or processing power requirements. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - You can change the instance memory size at any time. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - Instance resources are shared between your function code and the Functions host.
- The larger the instance memory size, the more each instance can handle as far as concurrent executions or more intensive CPU or memory workloads. Specific scale decisions are workload-specific.
- The default concurrency of HTTP triggers depends on the instance memory size. For more information, see
[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency). - Available CPUs and network bandwidth are provided proportional to a specific instance size.

## Per-function scaling

[Concurrency](#concurrency) is a key factor that determines how Flex Consumption function apps scale. To improve the scale performance of apps with various trigger types, the Flex Consumption plan provides a more deterministic way of scaling your app on a per-function basis.

This *per-function scaling* behavior is a part of the hosting platform, so you don't need to configure your app or change the code. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling) in the Event-driven scaling article.

In per-function scaling, decisions are made for certain function triggers based on group aggregations. This table shows the defined set of function scale groups:

| Scale groups | Triggers in group | Settings value |
|---|---|---|
| HTTP triggers |
|

`http`

(Event Grid-based)

[Blob storage trigger](functions-bindings-storage-blob-trigger)`blob`

[Orchestration trigger](durable/durable-functions-bindings#orchestration-trigger)[Activity trigger](durable/durable-functions-bindings#activity-trigger)[Entity trigger](durable/durable-functions-bindings#entity-trigger)`durable`

All other functions in the app are scaled individually in their own set of instances, which are referenced using the convention `function:<NAMED_FUNCTION>`

.

## Always ready instances

Flex Consumption includes an *always ready* feature that lets you choose instances that are always running and assigned to each of your per-function scale groups or functions. Always ready is a great option for scenarios where you need to have a minimum number of instances always ready to handle requests. For example, to reduce your application's cold start latency. The default is 0 (zero).

For example, if you set always ready to 2 for your HTTP group of functions, the platform keeps two instances always running for those functions. Those instances process your function executions first. Depending on concurrency settings, the platform scales beyond those two instances with on-demand instances.

No less than two always-ready instances can be configured per function or function group while [zone redundancy is enabled](/en-us/azure/reliability/reliability-functions?pivots=flex-consumption-plan#availability-zone-support).

To learn how to configure always ready instances, see [Set always ready instance counts](flex-consumption-how-to#set-always-ready-instance-counts).

## Concurrency

Concurrency refers to the number of parallel executions of a function on an instance of your app. You can set a maximum number of concurrent executions that each instance should handle at any given time. Concurrency has a direct effect on how your app scales because at lower concurrency levels, you need more instances to handle the event-driven demand for a function. While you can control and fine tune the concurrency, we provide defaults that work for most cases.

To learn how to set concurrency limits for HTTP trigger functions, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits). To learn how to set concurrency limits for non-HTTP trigger functions, see [Target Base Scaling](functions-target-based-scaling).

## Deployment

Deployments in the Flex Consumption plan follow a single path, and there's no longer the need for app settings to influence deployment behavior. Your project code is built and zipped into an application package, then deployed to a blob storage container. On startup, your app gets the package and runs your function code from this package. By default, the same storage account used to store internal host metadata (AzureWebJobsStorage) is also used as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by [configuring your app's deployment settings](flex-consumption-how-to#configure-deployment-settings).

Tip

A **Flex Consumption Deployment** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Consumption Deployment`

. This tool displays detailed information about your deployments, including deployment history, package status, and troubleshooting recommendations.

### Zero-downtime deployments

Note

Zero-downtime deployments with rolling updates are currently in public preview.

Flex Consumption provides zero-downtime deployments through rolling updates as the [site update strategy](flex-consumption-site-updates), which allows code deployments and configuration changes to be applied gradually across instances without interrupting function execution. Other hosting plans use deployment slots to minimize downtime during deployments. For deployment options across all hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments).

## Billing

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

The minimum billable execution period for both execution modes is 1,000 ms. Past that, the billable activity period is rounded up to the nearest 100 ms. You can find details on the Flex Consumption plan billing meters in the [Monitoring reference](monitor-functions-reference?tab=flex-consumption-plan#metrics).

For details about how costs are calculated when you run in a Flex Consumption plan, including examples, see [Consumption-based costs](functions-consumption-costs?tabs=flex-consumption-plan#consumption-based-costs) and [Viewing cost-related data](functions-consumption-costs?tabs=flex-consumption-plan#viewing-and-estimating-costs-from-metrics).

## Supported language stack versions

This table shows the language stack versions that are currently supported for Flex Consumption apps:

| Language stack | Required version |
|---|---|
C# (isolated worker model)1 |
.NET 8, .NET 9, .NET 10 |
| Java | Java 11, Java 17, Java 21 |
| Node.js | Node.js 20, Node.js 22 |
| PowerShell | PowerShell 7.4 |
| Python | Python 3.10, Python 3.11, Python 3.12 |

- The
[C# in-process model](functions-dotnet-class-library)isn't supported. You instead need to[migrate your .NET project to the isolated worker model](migrate-dotnet-to-isolated-model).

## Regional subscription memory quotas

All Flex Consumption apps in a subscription and region share a compute quota, like a shared bucket of resources. This quota applies only to Flex Consumption apps — other hosting plans like Consumption, Premium, and Dedicated don't count against it. The quota limits how much total compute your Flex Consumption apps can use at the same time. If your apps try to exceed the quota, some executions and deployments might be delayed or fail, and scaling is throttled. However, you can still create new apps.

### Default quota

Each region in a subscription has a default quota of **250 cores** (equivalent to **512,000 MB**) for all Flex Consumption app instances combined. You can use any combination of instance sizes and counts, as long as the total cores stay under the quota.

To calculate the cores used, multiply the cores per instance by the number of instances:

| Instance size | Cores per instance | Formula |
|---|---|---|
| 512 MB | 0.25 | instances × 0.25 |
| 2,048 MB | 1 | instances × 1 |
| 4,096 MB | 2 | instances × 2 |

### Quota examples

Each of these scenarios reaches the 250 core quota limit. When the quota is reached, apps in the region stop scaling:

| Scenario | Calculation | Total cores |
|---|---|---|
| One 512-MB app at 1,000 instances | 1,000 × 0.25 | 250 |
| Two 512-MB apps at 250 and 750 instances | (250 + 750) × 0.25 | 250 |
| One 2,048-MB app at 250 instances | 250 × 1 | 250 |
| Two 2,048-MB apps at 100 and 150 instances | (100 + 150) × 1 | 250 |
| One 4,096-MB app at 125 instances | 125 × 2 | 250 |
| One 4,096-MB app at 100 instances + one 2,048-MB app at 50 instances | (100 × 2) + (50 × 1) | 250 |

### Important notes

- Flex Consumption scales rapidly based on
[concurrency](#concurrency)settings, so apps frequently acquire and release cores from the quota as demand changes. - Flex Consumption apps that scale to zero, or instances marked to be scaled in and deleted, don't count against the quota.
- Always ready instances count against quota.
- A
**Flex Consumption Quota tool**is available in the Azure portal. Open any Flex Consumption app in your subscription, select**Diagnose and solve problems**, search for`Flex Consumption Quota`

, then choose a region. The tool displays recommendations, current quota information, and historical usage views. - This quota can be increased pending capacity review. For example, from 250 cores to 1,000 cores or more. To request a larger quota, create a support ticket or contact your Microsoft account team.

## Deprecated properties and settings

In the Flex Consumption plan, many standard application settings and site configuration properties are deprecated or moved. Don't use these settings when you automate function app resource creation. For more information, see [Flex Consumption plan deprecations](functions-app-settings#flex-consumption-plan-deprecations).

## Considerations

Keep these other considerations in mind when using Flex Consumption plan:

**Apps per Plan**: Only one app is allowed per Flex Consumption plan.**Host**: There's a 30-second time-out for app initialization. When your function app takes longer than 30 seconds to start, you might see gRPC-related`System.TimeoutException`

entries logged. You can't currently configure this time-out. For more information, see[this host work item](https://github.com/Azure/azure-functions-host/issues/10482).**Durable Functions**: Azure Storage and Durable Task Scheduler are the only supported[storage providers](durable/durable-functions-storage-providers)for Durable Functions when hosted in the Flex Consumption plan. See[recommendations](durable/durable-functions-azure-storage-provider#flex-consumption-plan)when hosting Durable Functions in the Flex Consumption plan.**Virtual network integration and Resource provider registration**: You must have the`Microsoft.App`

Azure resource provider registered in your subscription to integrate to a virtual network, which is needed for subnet delegation. The Azure portal and Azure CLI enforce registration at app creation time since virtual network integration can be enabled at any point after your app is created. To register this provider,[follow these instructions](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider). The subnet delegation required by Flex Consumption apps is`Microsoft.App/environments`

.**Triggers**: While all triggers are fully supported in a Flex Consumption plan, the Blob storage trigger only supports the[Event Grid source](functions-event-grid-blob-trigger). Non-C# function apps must use version`[4.0.0, 5.0.0)`

of the[extension bundle](extension-bundles), or a later version.**Regions**: While the Flex Consumption plan is available in many Azure regions, not all regions are currently supported. To learn more, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Deployments**: Deployment slots aren't currently supported. For zero downtime deployments with Flex Consumption, see[Site update strategies in Flex Consumption](flex-consumption-site-updates).**Azure Storage as a local share**: Network File System (NFS) file shares aren't available for Flex Consumption. Only Server Message Block (SMB) and Azure Blobs (read-only) are supported.**Scale**: The lowest maximum scale is currently`40`

. The highest currently supported value is`1000`

.**PowerShell Managed dependencies**: Flex Consumption doesn't support[managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature). You must instead[upload modules with app content](functions-reference-powershell#including-modules-in-app-content).**Certificates**: Loading certificates with the WEBSITE_LOAD_CERTIFICATES app setting, managed certificates, app service certificates, and other platform certificate-based features like endToEndEncryptionEnabled are currently not supported.**Timezones**:`WEBSITE_TIME_ZONE`

and`TZ`

app settings aren't currently supported when running on Flex Consumption plan.**Azure Functions Runtime Version and Proxies**: Flex Consumption only supports version 4.x and later of the Azure Functions runtime. Azure Functions proxies was a feature of versions 1.x through 3.x of the Azure Functions runtime and is not available in Flex Consumption.

## Related articles

[Azure Functions hosting options](functions-scale)
[Create and manage function apps in the Flex Consumption plan](flex-consumption-how-to)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs -->

# Develop Azure Functions using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Visual Studio provides a way to develop, test, and deploy C# class library functions to Azure. If this experience is your first with Azure Functions, see [Azure Functions overview](functions-overview).

To get started right away, consider completing the [Functions quickstart for Visual Studio](functions-create-your-first-function-visual-studio).

This article provides detailed information about how to use Visual Studio to develop C# class library functions and publish them to Azure.
There are two models for developing C# class library functions: the [isolated worker model](dotnet-isolated-process-guide) and the [in-process model](functions-dotnet-class-library).

You're reading the isolated worker model version of this article. You can select your preferred model at the top of the article.

You're reading the in-process model version of this article. You can select your preferred model at the top of the article.

Important

[Support for the in-process model ends on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We recommend that you [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

Unless otherwise noted, procedures and examples shown are for Visual Studio 2022. For more information about Visual Studio 2022 releases, see the [release notes](/en-us/visualstudio/releases/2022/release-notes) or the [preview release notes](/en-us/visualstudio/releases/2022/release-notes-preview).

## Prerequisites

Visual Studio 2022, including the

**Azure development**workload.Other resources that you need, such as an Azure Storage account, are created in your subscription during the publishing process.

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Functions project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In the

**Create a new project**dialog, enter**functions**in the search box, select the**Azure Functions**template, and then select**Next**.In the

**Configure your new project**dialog, for**Project name**, enter a name for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.In the

**Additional information**dialog, take the actions listed in the following table:Setting Action Description **Functions worker**Select **.NET 8.0 Isolated (Long Term Support)**.Visual Studio creates a function project that runs in an [isolated worker process](dotnet-isolated-process-guide). The isolated worker process also supports other versions of .NET and .NET Framework that don't offer long term support (LTS). For more information, see[Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**.When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Setting Action Description **Functions worker**Select **.NET 8.0 In-process (Long Term Support)**.Visual Studio creates a function project that runs in-process with version 4.x of the Functions runtime. For more information, see [Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you select the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint.Select

**Create**to create the function project and HTTP trigger function.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.Azure.Functions.Worker`

and `Microsoft.Azure.Functions.Worker.Sdk`

NuGet packages, and sets the target framework.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.NET.Sdk.Functions`

NuGet package, and sets the target framework.

The new project has the following files:

*host.json*: This file provides a way for you to configure the Functions host. These settings apply both when running locally and in Azure. For more information, see[host.json reference](functions-host-json).*local.settings.json*: This file maintains settings that you use when you run functions locally. These settings aren't used when your app runs in Azure. For more information, see[Work with app settings locally](#local-settings).Important

Because the

*local.settings.json*file can contain secrets, you must exclude it from your project source control. In the**Properties**dialog for this file, make sure the**Copy to Output Directory**setting is set to**Copy if newer**.

For more information, see [Project structure](dotnet-isolated-process-guide#project-structure) in the isolated worker guide.

For more information, see [Functions class library project](functions-dotnet-class-library#functions-class-library-project).

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

Visual Studio doesn't automatically upload the settings in *local.settings.json* when you publish the project. To make sure that these settings also exist in your function app in Azure, upload them after you publish your project. For more information, see [Function app settings](#function-app-settings). The values in a `ConnectionStrings`

collection aren't published.

Your code can also read the function app settings values as environment variables. For more information, see [Environment variables](functions-dotnet-class-library#environment-variables).

## Configure the project for local development

The Functions runtime uses a Storage account internally. During development, you can use a valid Storage account for this internal account, or you can use the [Azurite emulator](../storage/common/storage-use-azurite).

For all trigger types other than HTTP and webhooks, you need to set the value of the `Values.AzureWebJobsStorage`

key in the *local.settings.json* file:

- For a Storage account, set the value to the connection string of your storage account.
- For the emulator, set the value to
`UseDevelopmentStorage=true`

.

If you use the emulator, change this setting to an actual storage account connection string before deployment. For more information, see [Local storage emulator](functions-develop-local#local-storage-emulator).

To set the storage account connection string, take the following steps:

Sign in to the

[Azure portal](https://portal.azure.com), and then go to your storage account.Select

**Security + networking**>**Access keys**. Under**key1**, copy the**Connection string**value.In your Visual Studio project, open the

*local.settings.json*file. Set the value of the`AzureWebJobsStorage`

key to the connection string you copied.Repeat the previous step to add unique keys to the

`Values`

array for any other connections required by your functions.

## Add a function to your project

In C# class library functions, the bindings that the functions use are defined by applying attributes in the code. When you create your function triggers from the provided templates, the trigger attributes are applied for you.

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.In the

**Add New Item**dialog, select**Azure Function**, and then select**Add**.Select a trigger, and then set the required binding properties. If you select a Storage service trigger and you want to configure the connection, select the checkbox for configuring the trigger connection. The following example shows the settings for creating a Queue Storage trigger function.

Select

**Add**. If you select the checkbox for configuring a storage connection in the previous step, the**Connect to dependency**page appears. Select an Azurite storage emulator or**Azure Storage**, and then select**Next**.- If you select an Azurite storage emulator, the
**Connect to Storage Azurite emulator**page appears. Take the following steps:- Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select
- If you select
**Azure Storage**, the**Connect to Azure Storage**page appears. Take the following steps:- Select a storage account, and then select
**Next**. Visual Studio tries to connect to your Azure account and retrieve an endpoint. - Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select a storage account, and then select

This trigger example uses an application setting for the storage connection with a key named

`QueueStorage`

. This key, stored in the[local.settings.json file](functions-develop-local#local-settings-file), either references the Azurite emulator or a Storage account.- If you select an Azurite storage emulator, the
Examine the newly added class. For example, the following C# class represents a basic Queue Storage trigger function:

A

`Run()`

method is attributed with`Function`

. This attribute indicates that the method is the entry point for the function.`using System; using Azure.Storage.Queues.Models; using Microsoft.Azure.Functions.Worker; using Microsoft.Extensions.Logging; namespace Company.Function; public class QueueTriggerCSharp { private readonly ILogger<QueueTriggerCSharp> _logger; public QueueTriggerCSharp(ILogger<QueueTriggerCSharp> logger) { _logger = logger; } [Function(nameof(QueueTriggerCSharp))] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")] QueueMessage message) { _logger.LogInformation("C# Queue trigger function processed: {messageText}", message.MessageText); } }`

A static

`Run()`

method is attributed with`FunctionName`

. This attribute indicates that the method is the entry point for the function.`using System; using Microsoft.Azure.WebJobs; using Microsoft.Azure.WebJobs.Host; using Microsoft.Extensions.Logging; namespace Company.Function { public class QueueTriggerCSharp { [FunctionName("QueueTriggerCSharp")] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")]string myQueueItem, ILogger log) { log.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); } } }`


A binding-specific attribute is applied to each binding parameter supplied to the entry point method. The attribute takes the binding information as parameters.

In the preceding code, the first parameter has a `QueueTrigger`

attribute applied, which indicates a Queue Storage trigger function. The queue name and connection string setting name are passed as parameters to the `QueueTrigger`

attribute. In your class:

- The queue name parameter should match the name of the queue you use in an earlier step to create the trigger, such as
`myqueue-items`

. - The connection string setting name should match the one you use in an earlier step to create the trigger, such as
`QueueStorage`

.

For more information, see [Azure Queue storage trigger for Azure Functions](functions-bindings-storage-queue-trigger).

Use the preceding procedure to add more functions to your function app project. Each function in the project can have a different trigger, but a function must have exactly one trigger. For more information, see [Azure Functions triggers and bindings](functions-triggers-bindings).

## Add bindings

As with triggers, input and output bindings are added to your function as binding attributes. To add bindings to a function, take the following steps:

Make sure you

[configure the project for local development](#configure-the-project-for-local-development).Add the appropriate NuGet extension package for each specific binding. For binding-specific NuGet package requirements, see the reference article for the binding. For example, for package requirements for the Azure Event Hubs trigger, see

[Azure Event Hubs trigger and bindings for Azure Functions](functions-bindings-event-hubs).Use the following command in the Package Manager Console to install a specific package:

`Install-Package Microsoft.Azure.Functions.Worker.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

`Install-Package Microsoft.Azure.WebJobs.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

In this code, replace

`<BINDING_TYPE>`

with the specific name of the binding extension, and replace`<TARGET_VERSION>`

with a specific version of the package, such as`4.0.0`

. Valid versions are listed on the individual package pages at[NuGet.org](https://nuget.org).If there are app settings that the binding needs, add them to the

`Values`

collection in the[local setting file](functions-develop-local#local-settings-file).The function uses these values when it runs locally. When the function runs in the function app in Azure, it uses the

[function app settings](#function-app-settings). Visual Studio makes it easy to[publish local settings to Azure](#function-app-settings).Add the appropriate binding attribute to the method signature. In the following code, a queue message triggers the

`Run`

function. The output binding then creates a new queue message with the same text in a different queue.`public class QueueTrigger { private readonly ILogger _logger; public QueueTrigger(ILoggerFactory loggerFactory) { _logger = loggerFactory.CreateLogger<QueueTrigger>(); } [Function("CopyQueueMessage")] [QueueOutput("myqueue-items-destination", Connection = "QueueStorage")] public string Run([QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem) { _logger.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); return myQueueItem; } }`

The

`QueueOutput`

attribute defines the binding on the method. For multiple output bindings, you instead place this attribute on a string property of the returned object. For more information, see[Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).`public static class SimpleExampleWithOutput { [FunctionName("CopyQueueMessage")] public static void Run( [QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem, [Queue("myqueue-items-destination", Connection = "QueueStorage")] out string myQueueItemCopy, ILogger log) { log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}"); myQueueItemCopy = myQueueItem; } }`

The

`Queue`

attribute on the`out`

parameter defines the output binding.The connection to Queue Storage is obtained from the

`QueueStorage`

setting. For more information, see the reference article for the specific binding.

For a full list of the bindings supported by Functions, see [Supported bindings](functions-triggers-bindings?tabs=csharp#supported-bindings). For a more complete example of this scenario, see [Connect functions to Azure Storage using Visual Studio](functions-add-output-binding-storage-queue-vs).

## Run functions locally

You can use Azure Functions Core Tools to run Functions projects on your local development computer. When you select **F5** to debug a Functions project, the local Functions host (`func.exe`

) starts to listen on a local port (usually 7071). Any callable function endpoints are written to the output, and you can use these endpoints for testing your functions. For more information, see [Develop Azure Functions locally using Core Tools](functions-run-local). You're prompted to install these tools the first time you start a function from Visual Studio.

Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If you use an earlier version, the

`func start`

command generates an error.To start your function in Visual Studio in debug mode, take the following steps:

Select

**F5**. If prompted, accept the request from Visual Studio to download and install Azure Functions Core Tools. You might also need to turn on a firewall exception so that the tools can handle HTTP requests.When the project runs, test your code the same way you test a deployed function.

When you run Visual Studio in debug mode, breakpoints are hit as expected.


For a more detailed testing scenario that uses Visual Studio, see [Test functions](#test-functions), later in this article.

## Publish to Azure

When you publish your Functions project to Azure, Visual Studio uses [zip deployment](functions-deployment-technologies#zip-deploy) to deploy the project files. When possible, you should also select **Run from package file** so that the project runs in the deployment (.zip) package. For more information, see [Run your functions from a package file in Azure](run-functions-from-deployment-package).

Don't deploy to Functions by using Web Deploy (`msdeploy`

).

Use the following steps to publish your project to a function app in Azure:

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).[Application Insights](functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Function app settings

Visual Studio doesn't upload app settings automatically when you publish your project. If you add settings to the *local.settings.json* file, you must also add them to the function app in Azure.

The easiest way to upload the required settings to your function app in Azure is to manage them in Visual Studio. On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Manage Azure App Service settings**.

When you make the selection, the **Application settings** dialog opens for the function app. You can use this dialog to add application settings or modify existing ones.


For each setting, the **Local** value is the value in the *local.settings.json* file, and the **Remote** value is the value in the function app in Azure.

- To create an app setting, select
**Add setting**. - To copy a setting value from the
**Local**field to the**Remote**field, select**Insert value from Local**.

Pending changes are written to the local settings file and the function app when you select **OK**.

Note

By default, the *local.settings.json* file isn't checked into source control. As a result, if you clone a local Functions project from source control, the project doesn't have a *local.settings.json* file. You need to manually create the *local.settings.json* file in the project root so that the **Application settings** dialog works as expected.

You can also manage application settings in one of these other ways:

- Use the
[Azure portal](functions-how-to-use-azure-function-app-settings#settings). - Use the
.`--publish-local-settings`

publish option in the Azure Functions Core Tools - Use the
[Azure CLI](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set).

## Remote debugging

To debug your function app remotely, you must publish a debug configuration of your project. You also need to turn on remote debugging in your function app in Azure.

This section assumes a debug configuration to your function app is published.

### Remote debugging considerations

- Remote debugging isn't recommended on a production service.
- To use remote debugging, you must host your function app in a Premium or App Service plan.
- Remote debugging is currently only supported when running your C# app on Windows.
- If you have the Just My Code feature turned on in Visual Studio, turn it off. For instructions, see
[Enable or disable Just My Code](/en-us/visualstudio/debugger/just-my-code#BKMK_Enable_or_disable_Just_My_Code). - Avoid long stops at breakpoints when you use remote debugging. When a process is stopped for longer than a few minutes, Azure treats it as an unresponsive process and shuts it down.
- While you're debugging, the server sends data to Visual Studio, which can affect bandwidth charges. For information about bandwidth rates, see
[Pricing calculator](https://azure.microsoft.com/pricing/calculator/). - Remote debugging is automatically turned off in your function app after 48 hours. After that point, you need to turn remote debugging back on.

### Attach the debugger

When you debug an isolated worker process app, you currently need to attach the remote debugger to a separate .NET process. Several other configuration steps are also required.

To attach a remote debugger to a function app running in a process separate from the Functions host, take the following steps:

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Attach debugger**.Visual Studio connects to your function app and turns on remote debugging if it's not already turned on.

Note

Because the remote debugger can't connect to the host process, an error message might appear. In any case, the local debugger can't access your breakpoints or provide a way for you to inspect variables or step through code.

On the Visual Studio

**Debug**menu, select**Attach to Process**.In the

**Attach to Process**dialog, take the following steps:- Next to
**Connection type**, select**Microsoft Azure App Services**. - Next to
**Connection target**, select**Find**.

- Next to
In the

**Azure Attach to Process**dialog, search for and select your function app, and then select**OK**.If prompted, allow Visual Studio access through your local firewall.

Back in the

**Attach to Process**dialog, select**Show processes for all users**. Select**dotnet.exe**, and then select**Attach**.

When the operation finishes, you're attached to your C# class library code running in an isolated worker process. At this point, you can debug your function app as normal.

To attach a remote debugger to a function app running in-process with the Functions host, take the following steps.

On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Attach debugger**.

Visual Studio connects to your function app and turns on remote debugging if it's not already turned on. It also locates and attaches the debugger to the host process for the app. At this point, you can debug your function app as normal.

When you finish debugging, you should [turn off remote debugging](#turn-off-remote-debugging).

### Turn off remote debugging

After you finish remote debugging your code, you should turn off remote debugging in the [Azure portal](https://portal.azure.com). Remote debugging is automatically turned off after 48 hours, in case you forget.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The Azure portal opens to the function app your project is deployed to.In the function app, select

**Settings**>**Configuration**, and then go to the**General settings**tab. Next to**Remote debugging**, select**Off**. Select**Save**, and then select**Continue**.

After the function app restarts, you can no longer remotely connect to your remote processes. You can use this same tab in the Azure portal to turn on remote debugging outside of Visual Studio.

## Monitor functions

The recommended way to monitor your functions is by integrating your function app with Application Insights. You should turn on this integration when you create your function app during Visual Studio publishing.

If the integration isn't set up during publishing for some reason, you should still turn on [Application Insights integration](configure-monitoring#enable-application-insights-integration) for your function app in Azure.

For more information about using Application Insights for monitoring, see [Monitor executions in Azure Functions](functions-monitoring).

## Test functions

This section describes how to create a C# in-process model project that you can test by using [xUnit](https://github.com/xunit/xunit), an open-source unit testing tool for .NET.

### Step 1: Setup

Follow these steps to configure the environment, including the app project and functions, required to support your tests:

In Visual Studio, create an Azure Functions project named

**Functions**.Create an HTTP function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Http trigger**, and then select**Add**. - Rename the new class
*MyHttpTrigger*.

- In
Create a timer function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Timer trigger**, and then select**Add**. - Rename the new class
*MyTimerTrigger*.

- In
Create an

[xUnit Test app](https://xunit.net/docs/getting-started/v3/getting-started)in the solution:- In
**Solution Explorer**, right-click the solution that contains your**Functions**project, and then select**Add**>**New Project**. - Select the
**xUnit Test Project**template, and then select**Next**. - Name the project
**Functions.Tests**.

- In
Remove the default test files from the

**Functions.Tests**project.Use NuGet to add a reference from the test app to

[Microsoft.AspNetCore.Mvc](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc/). You can use Package Manager Console, or you can take the following steps:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Manage NuGet Packages**. - Search for and install
**Microsoft.AspNetCore.Mvc**.

- In
In the

**Functions.Tests**app,[add a reference](/en-us/visualstudio/ide/managing-references-in-a-project)to the**Functions**app:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Add**>**Project Reference**. - Select the
**Functions**project, and then select**OK**.

- In

### Step 2: Create test classes

In this section, you create the classes that you use to run the automated tests.

Each function takes an implementation of [ ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) to handle message logging. In some tests, no messages are logged, or it doesn't matter how logging is implemented. Other tests need to evaluate logged messages to determine whether a test should pass.

Create a class in your

**Functions.Tests**project named`NullScope`

and add the following code. This class provides a mock scope. In a later step, you create an implementation of`ILogger`

that uses this scope.`using System; namespace Functions.Tests { public class NullScope : IDisposable { public static NullScope Instance { get; } = new NullScope(); private NullScope() { } public void Dispose() { } } }`

Create a class in your

**Functions.Tests**project named`ListLogger`

and add the following code. This class maintains an internal list of messages to evaluate during testing. To implement the required`ILogger`

interface, the class uses the mock scope from the`NullScope`

class. The test cases pass the mock scope to the`ListLogger`

class.`using Microsoft.Extensions.Logging; using System; using System.Collections.Generic; using System.Text; namespace Functions.Tests { public class ListLogger : ILogger { public IList<string> Logs; public IDisposable BeginScope<TState>(TState state) => NullScope.Instance; public bool IsEnabled(LogLevel logLevel) => false; public ListLogger() { this.Logs = new List<string>(); } public void Log<TState>(LogLevel logLevel, EventId eventId, TState state, Exception exception, Func<TState, Exception, string> formatter) { string message = formatter(state, exception); this.Logs.Add(message); } } }`

The

`ListLogger`

class implements the following members, as contracted by the`ILogger`

interface:`BeginScope`

: Scopes add context to your logging. In this case, the test points to the static instance on the`NullScope`

class to allow the test to function.`IsEnabled`

: A default value of`false`

is provided.`Log`

: This method uses the provided`formatter`

function to format the message. The method then adds the resulting text to the`Logs`

collection.

The

`Logs`

collection is an instance of`List<string>`

and is initialized in the constructor.Create a code file in the

**Functions.Tests**project named*LoggerTypes.cs*and add the following code:`namespace Functions.Tests { public enum LoggerTypes { Null, List } }`

This enumeration specifies the type of logger that the tests use.

Create a class in the

**Functions.Tests**project named`TestFactory`

and add the following code:`using Microsoft.AspNetCore.Http; using Microsoft.AspNetCore.Http.Internal; using Microsoft.Extensions.Logging; using Microsoft.Extensions.Logging.Abstractions; using Microsoft.Extensions.Primitives; using System.Collections.Generic; namespace Functions.Tests { public class TestFactory { public static IEnumerable<object[]> Data() { return new List<object[]> { new object[] { "name", "Bernardo" }, new object[] { "name", "Ananya" }, new object[] { "name", "Vlad" } }; } private static Dictionary<string, StringValues> CreateDictionary(string key, string value) { var qs = new Dictionary<string, StringValues> { { key, value } }; return qs; } public static HttpRequest CreateHttpRequest(string queryStringKey, string queryStringValue) { var context = new DefaultHttpContext(); var request = context.Request; request.Query = new QueryCollection(CreateDictionary(queryStringKey, queryStringValue)); return request; } public static ILogger CreateLogger(LoggerTypes type = LoggerTypes.Null) { ILogger logger; if (type == LoggerTypes.List) { logger = new ListLogger(); } else { logger = NullLoggerFactory.Instance.CreateLogger("Null Logger"); } return logger; } } }`

The

`TestFactory`

class implements the following members:`Data`

: This property returns an[IEnumerable](/en-us/dotnet/api/system.collections.ienumerable)collection of sample data. The key-value pairs represent values that are passed into a query string.`CreateDictionary`

: This method accepts a key-value pair as an argument. It returns a new instance of`Dictionary`

that's used to create an instance of`QueryCollection`

to represent query string values.`CreateHttpRequest`

: This method creates an HTTP request that's initialized with the given query string parameters.`CreateLogger`

: This method returns an implementation of`ILogger`

that's used for testing. The`ILogger`

implementation depends on the specified logger type. If a list type is specified, the`ListLogger`

instance keeps track of logged messages that are available for evaluation in tests.

Create a class in the

**Functions.Tests**project named`FunctionsTests`

and add the following code:`using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Logging; using Xunit; namespace Functions.Tests { public class FunctionsTests { private readonly ILogger logger = TestFactory.CreateLogger(); [Fact] public async void Http_trigger_should_return_known_string() { var request = TestFactory.CreateHttpRequest("name", "Bernardo"); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal("Hello, Bernardo. This HTTP triggered function executed successfully.", response.Value); } [Theory] [MemberData(nameof(TestFactory.Data), MemberType = typeof(TestFactory))] public async void Http_trigger_should_return_known_string_from_member_data(string queryStringKey, string queryStringValue) { var request = TestFactory.CreateHttpRequest(queryStringKey, queryStringValue); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal($"Hello, {queryStringValue}. This HTTP triggered function executed successfully.", response.Value); } [Fact] public void Timer_should_log_message() { var logger = (ListLogger)TestFactory.CreateLogger(LoggerTypes.List); new MyTimerTrigger().Run(null, logger); var msg = logger.Logs[0]; Assert.Contains("C# Timer trigger function executed at", msg); } } }`

This class implements the following members:

`Http_trigger_should_return_known_string`

: This test uses the query string value`name=Bernardo`

to create a request to an HTTP function. This test checks that the expected response is returned.`Http_trigger_should_return_string_from_member_data`

: This test uses xUnit attributes to provide sample data to the HTTP function.`Timer_should_log_message`

: This test creates an instance of`ListLogger`

and passes it to a timer function. After the function runs, the log is checked to make sure the expected message is present.

To access application settings in your tests, you can

[inject](functions-dotnet-dependency-injection)an`IConfiguration`

implementation with mocked environment variable values into your function.

### Step 3: Run tests

To run the tests in Visual Studio, select **View** > **Test Explorer**. In **Test Explorer**, select **Run** > **Run All Tests in View**.


### Step 4: Debug tests

To debug the tests, set a breakpoint on a test. In **Test Explorer**, select **Run** > **Debug Last Run**.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-cosmos-db-vs-code -->

# Connect Azure Functions to Azure Cosmos DB using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

This article shows you how to use Visual Studio Code to connect [Azure Cosmos DB](/en-us/azure/cosmos-db/introduction) to the function you created in the previous quickstart article. The output binding that you add to this function writes data from the HTTP request to a JSON document stored in an Azure Cosmos DB container.

Before you begin, you must complete the [quickstart: Create a C# function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Before you begin, you must complete the [quickstart: Create a JavaScript function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-javascript?pivot=nodejs-model-v3). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

Note

This article currently only supports [Node.js v3 for Functions](functions-reference-node?pivots=nodejs-model-v3).

Before you begin, you must complete the [quickstart: Create a Python function in Azure using Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-python). If you already cleaned up resources at the end of that article, go through the steps again to recreate the function app and related resources in Azure.

## Configure your environment

Before you get started, make sure to install the [Azure Databases extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb) for Visual Studio Code.

## Create your Azure Cosmos DB account

Now, you create an Azure Cosmos DB account as a [serverless account type](/en-us/azure/cosmos-db/serverless). This consumption-based mode makes Azure Cosmos DB a strong option for serverless workloads.

In Visual Studio Code, select

**View**>**Command Palette...**then in the command palette search for`Azure Databases: Create Server...`

Provide the following information at the prompts:

Prompt Selection **Select an Azure Database Server**Choose **Core (NoSQL)**to create a document database that you can query by using a SQL syntax or a Query Copilot ([Preview](/en-us/azure/cosmos-db/nosql/query/how-to-enable-use-copilot)) converting natural language prompts to queries.[Learn more about the Azure Cosmos DB](/en-us/azure/cosmos-db/introduction).**Account name**Enter a unique name to identify your Azure Cosmos DB account. The account name can use only lowercase letters, numbers, and hyphens (-), and must be between 3 and 31 characters long. **Select a capacity model**Select **Serverless**to create an account in[serverless](/en-us/azure/cosmos-db/serverless)mode.**Select a resource group for new resources**Choose the resource group where you created your function app in the [previous article](how-to-create-function-vs-code?pivot=programming-language-csharp).**Select a location for new resources**Select a geographic location to host your Azure Cosmos DB account. Use the location that's closest to you or your users to get the fastest access to your data. After your new account is provisioned, a message is displayed in notification area.


## Create an Azure Cosmos DB database and container

Select the Azure icon in the Activity bar, expand

**Resources**>**Azure Cosmos DB**, right-click (Ctrl+select on macOS) your account, and select**Create database...**.Provide the following information at the prompts:

Prompt Selection **Database name**Type `my-database`

.**Enter and ID for your collection**Type `my-container`

.**Enter the partition key for the collection**Type `/id`

as the[partition key](/en-us/azure/cosmos-db/partitioning-overview).Select

**OK**to create the container and database.

## Update your function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure. In this article, you update your app to write JSON documents to the Azure Cosmos DB container you've created. To connect to your Azure Cosmos DB account, you must add its connection string to your app settings. You then download the new setting to your local.settings.json file so you can connect to your Azure Cosmos DB account when running locally.

In Visual Studio Code, right-click (Ctrl+select on macOS) on your new Azure Cosmos DB account, and select

**Copy Connection String**.Press

`F1`to open the command palette, then search for and run the command`Azure Functions: Add New Setting...`

.Choose the function app you created in the previous article. Provide the following information at the prompts:

Prompt Selection **Enter new app setting name**Type `CosmosDbConnectionString`

.**Enter value for "CosmosDbConnectionString"**Paste the connection string of your Azure Cosmos DB account you copied. You can also configure [Microsoft Entra identity](functions-bindings-cosmosdb-v2-trigger#connections)as an alternative.This creates an application setting named connection

`CosmosDbConnectionString`

in your function app in Azure. Now, you can download this setting to your local.settings.json file.Press

`F1`again to open the command palette, then search for and run the command`Azure Functions: Download Remote Settings...`

.Choose the function app you created in the previous article. Select

**Yes to all**to overwrite the existing local settings.

This downloads all of the setting from Azure to your local project, including the new connection string setting. Most of the downloaded settings aren't used when running locally.

## Register binding extensions

Because you're using an Azure Cosmos DB output binding, you must have the corresponding bindings extension installed before you run the project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Azure Cosmos DB extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.CosmosDB
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway"
}
}
}
```


Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles usage is enabled in the *host.json* file at the root of the project, which appears as follows:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


Now, you can add the Azure Cosmos DB output binding to your project.

## Add an output binding

In a C# class library project, the bindings are defined as binding attributes on the function method.

Open the *HttpExample.cs* project file and add the following classes:

```
public class MultiResponse
{
[CosmosDBOutput("my-database", "my-container",
Connection = "CosmosDbConnectionSetting", CreateIfNotExists = true)]
public MyDocument Document { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
public class MyDocument {
public string id { get; set; }
public string message { get; set; }
}
```


The `MyDocument`

class defines an object that gets written to the database. The connection string for the Storage account is set by the `Connection`

property. In this case, you could omit `Connection`

because you're already using the default storage account.

The `MultiResponse`

class allows you to both write to the specified collection in the Azure Cosmos DB and return an HTTP success message. Because you need to return a `MultiResponse`

object, you need to also update the method signature.

Specific attributes specify the name of the container and the name of its parent database. The connection string for your Azure Cosmos DB account is set by the `CosmosDbConnectionString`

.

Binding attributes are defined directly in your function code. The [Azure Cosmos DB output configuration](functions-bindings-cosmosdb-v2-output#configuration) describes the fields required for an Azure Cosmos DB output binding.

For this `MultiResponse`

scenario, you need to add an `extraOutputs`

output binding to the function.

```
app.http('HttpExample', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
```


Add the following properties to the binding configuration:

```
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
```


Binding attributes are defined directly in the *function_app.py* file. You use the `cosmos_db_output`

decorator to add an [Azure Cosmos DB output binding](functions-bindings-triggers-python#azure-cosmos-db-output-binding):

```
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database",
container_name="my-container", connection="CosmosDbConnectionString")
```


In this code, `arg_name`

identifies the binding parameter referenced in your code, `database_name`

and `container_name`

are the database and collection names that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Azure Cosmos DB account, which is in the `CosmosDbConnectionString`

setting in the *local.settings.json* file.

## Add code that uses the output binding

Replace the existing Run method with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and Azure Cosmos DB output binding.
return new MultiResponse()
{
Document = new MyDocument
{
id = System.Guid.NewGuid().ToString(),
message = message
},
HttpResponse = response
};
}
```


Add code that uses the `extraInputs`

output binding object on `context`

to send a JSON document to the named output binding function, `sendToCosmosDb`

. Add this code before the `return`

statement.

```
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
```


At this point, your function should look as follows:

```
const { app, output } = require('@azure/functions');
const sendToCosmosDb = output.cosmosDB({
databaseName: 'my-database',
containerName: 'my-container',
createIfNotExists: false,
connection: 'CosmosDBConnectionString',
});
app.http('HttpExampleToCosmosDB', {
methods: ['GET', 'POST'],
extraOutputs: [sendToCosmosDb],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
if (!name) {
return { status: 404, body: 'Missing required data' };
}
// Output to Database
context.extraOutputs.set(sendToCosmosDb, {
// create a random ID
id:
new Date().toISOString() + Math.random().toString().substring(2, 10),
name: name,
});
const responseMessage = name
? 'Hello, ' +
name +
'. This HTTP triggered function executed successfully.'
: 'This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.';
// Return to HTTP client
return { body: responseMessage };
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


This code now returns a `MultiResponse`

object that contains both a document and an HTTP response.

Update *HttpExample\function_app.py* to match the following code. Add the `outputDocument`

parameter to the function definition and `outputDocument.set()`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.FUNCTION)
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
@app.cosmos_db_output(arg_name="outputDocument", database_name="my-database", container_name="my-container", connection="CosmosDbConnectionString")
def test_function(req: func.HttpRequest, msg: func.Out[func.QueueMessage],
outputDocument: func.Out[func.Document]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
logging.info('Python Cosmos DB trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
outputDocument.set(func.Document.from_dict({"id": name}))
msg.set(name)
return func.HttpResponse(f"Hello {name}!")
else:
return func.HttpResponse(
"Please pass a name on the query string or in the request body",
status_code=400
)
```


The document `{"id": "name"}`

is created in the database collection specified in the binding.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure. If you don't already have Core Tools installed locally, you are prompted to install it the first time you run your project.

To call your function, press

`F5`to start the function app project. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you don't already have Core Tools installed, select

**Install**to install Core Tools when prompted to do so.

If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to**WSL Bash**.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the`HttpExample`

function and choose**Execute Function Now...**.In the

**Enter request body**, press`Enter`to send a request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in the

**Terminal**panel.Press

`Ctrl + C`to stop Core Tools and disconnect the debugger.

## Run the function locally

As in the previous article, press

`F5`to start the function app project and Core Tools.With Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Ctrl-click on Mac) the`HttpExample`

function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.After a response is returned, press

`Ctrl + C`to stop Core Tools.

### Verify that a JSON document has been created

On the Azure portal, go back to your Azure Cosmos DB account and select

**Data Explorer**.Expand your database and container, and select

**Items**to list the documents created in your container.Verify that a new JSON document has been created by the output binding.


## Redeploy and verify the updated app

In Visual Studio Code, press F1 to open the command palette. In the command palette, search for and select

`Azure Functions: Deploy to function app...`

.Choose the function app that you created in the first article. Because you're redeploying your project to the same app, select

**Deploy**to dismiss the warning about overwriting files.After deployment completes, you can again use the

**Execute Function Now...**feature to trigger the function in Azure. This command automatically retrieves the function access key and uses it when calling the HTTP trigger endpoint.Again

[check the documents created in your Azure Cosmos DB container](#verify-that-a-json-document-has-been-created)to verify that the output binding again generates a new JSON document.

## Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write JSON documents to an Azure Cosmos DB container. Now you can learn more about developing Functions using Visual Studio Code:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan -->

# Azure Functions Flex Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Flex Consumption is a Linux-based Azure Functions hosting plan that builds on the Consumption *pay for what you use* serverless billing model. It gives you more flexibility and customizability by introducing private networking, instance memory size selection, and fast/large scale-out features still based on a *serverless* model.

You can review end-to-end samples that feature the Flex Consumption plan in the [Flex Consumption plan samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples).

## Benefits

The Flex Consumption plan builds on the strengths of the serverless Consumption plan, which include dynamic scaling and execution-based billing. With Flex Consumption, you also get these extra features:

**Reduced Cold Start Times**: Enable[always-ready instances](#always-ready-instances)to achieve faster cold-start times compared to the Consumption plan.**Virtual network support**:[Virtual network integration](#virtual-network-integration)enables your serverless app to run in a virtual network.**Per-Function Scaling**: Each function in your app[scales independently based on its workload](#per-function-scaling), potentially resulting in more efficient resource allocation.**Improved Concurrency Handling**: Better handling of concurrent executions with configurable concurrency settings per function.**Flexible Memory Configuration**: Flex Consumption offers multiple[instance sizes](#instance-sizes)size options, allowing you to optimize for your specific workload requirements.

This table helps you directly compare the features of Flex Consumption with the Consumption hosting plan:

| Feature | Consumption | Flex Consumption |
|---|---|---|
| Scale to zero | ✅ Yes | ✅ Yes |
| Scale behavior |
|

[Event driven](event-driven-scaling)(fast)For a complete comparison of the Flex Consumption plan against the Consumption plan and all other plan and hosting types, see [function scale and hosting options](functions-scale).

Tip

If you're migrating from the Linux Consumption plan, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux) for step-by-step migration instructions and important differences between the plans.

## Virtual network integration

Flex Consumption expands on the traditional benefits of Consumption plan by adding support for [virtual network integration](functions-networking-options#virtual-network-integration). When your apps run in a Flex Consumption plan, they can connect to other Azure services secured inside a virtual network. All while still allowing you to take advantage of serverless billing and scale, together with the scale and throughput benefits of the Flex Consumption plan. For more information, see [Enable virtual network integration](flex-consumption-how-to#enable-virtual-network-integration).

## Instance sizes

When you create your function app in a Flex Consumption plan, you can select the memory size of the instances on which your app runs. See [Billing](#billing) to learn how instance memory sizes affect the costs of your function app.

Currently, Flex Consumption offers these instance size options:

| Instance Memory (MB) | CPU Cores |
|---|---|
| 512 | 0.25 |
| 2048 | 1 |
| 4096 | 2 |

Note

The CPU core values shown are typical allocations for instances with the specified memory size. However, initial instances might be granted slightly different core allocations to improve performance. Each Flex Consumption instance also includes an extra 272 MB of memory allocated by the platform as a buffer for system and host processes. This extra memory doesn't affect billing, and instances are billed based on the configured instance memory size shown in the preceding table.

When deciding on which instance memory size to use with your apps, here are some things to consider:

- The 2,048-MB instance memory size is the default and should be used for most scenarios. The 512 MB and 4,096-MB instance memory sizes are available for scenarios that best suit your application's concurrency or processing power requirements. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - You can change the instance memory size at any time. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - Instance resources are shared between your function code and the Functions host.
- The larger the instance memory size, the more each instance can handle as far as concurrent executions or more intensive CPU or memory workloads. Specific scale decisions are workload-specific.
- The default concurrency of HTTP triggers depends on the instance memory size. For more information, see
[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency). - Available CPUs and network bandwidth are provided proportional to a specific instance size.

## Per-function scaling

[Concurrency](#concurrency) is a key factor that determines how Flex Consumption function apps scale. To improve the scale performance of apps with various trigger types, the Flex Consumption plan provides a more deterministic way of scaling your app on a per-function basis.

This *per-function scaling* behavior is a part of the hosting platform, so you don't need to configure your app or change the code. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling) in the Event-driven scaling article.

In per-function scaling, decisions are made for certain function triggers based on group aggregations. This table shows the defined set of function scale groups:

| Scale groups | Triggers in group | Settings value |
|---|---|---|
| HTTP triggers |
|

`http`

(Event Grid-based)

[Blob storage trigger](functions-bindings-storage-blob-trigger)`blob`

[Orchestration trigger](durable/durable-functions-bindings#orchestration-trigger)[Activity trigger](durable/durable-functions-bindings#activity-trigger)[Entity trigger](durable/durable-functions-bindings#entity-trigger)`durable`

All other functions in the app are scaled individually in their own set of instances, which are referenced using the convention `function:<NAMED_FUNCTION>`

.

## Always ready instances

Flex Consumption includes an *always ready* feature that lets you choose instances that are always running and assigned to each of your per-function scale groups or functions. Always ready is a great option for scenarios where you need to have a minimum number of instances always ready to handle requests. For example, to reduce your application's cold start latency. The default is 0 (zero).

For example, if you set always ready to 2 for your HTTP group of functions, the platform keeps two instances always running for those functions. Those instances process your function executions first. Depending on concurrency settings, the platform scales beyond those two instances with on-demand instances.

No less than two always-ready instances can be configured per function or function group while [zone redundancy is enabled](/en-us/azure/reliability/reliability-functions?pivots=flex-consumption-plan#availability-zone-support).

To learn how to configure always ready instances, see [Set always ready instance counts](flex-consumption-how-to#set-always-ready-instance-counts).

## Concurrency

Concurrency refers to the number of parallel executions of a function on an instance of your app. You can set a maximum number of concurrent executions that each instance should handle at any given time. Concurrency has a direct effect on how your app scales because at lower concurrency levels, you need more instances to handle the event-driven demand for a function. While you can control and fine tune the concurrency, we provide defaults that work for most cases.

To learn how to set concurrency limits for HTTP trigger functions, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits). To learn how to set concurrency limits for non-HTTP trigger functions, see [Target Base Scaling](functions-target-based-scaling).

## Deployment

Deployments in the Flex Consumption plan follow a single path, and there's no longer the need for app settings to influence deployment behavior. Your project code is built and zipped into an application package, then deployed to a blob storage container. On startup, your app gets the package and runs your function code from this package. By default, the same storage account used to store internal host metadata (AzureWebJobsStorage) is also used as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by [configuring your app's deployment settings](flex-consumption-how-to#configure-deployment-settings).

Tip

A **Flex Consumption Deployment** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Consumption Deployment`

. This tool displays detailed information about your deployments, including deployment history, package status, and troubleshooting recommendations.

### Zero-downtime deployments

Note

Zero-downtime deployments with rolling updates are currently in public preview.

Flex Consumption provides zero-downtime deployments through rolling updates as the [site update strategy](flex-consumption-site-updates), which allows code deployments and configuration changes to be applied gradually across instances without interrupting function execution. Other hosting plans use deployment slots to minimize downtime during deployments. For deployment options across all hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments).

## Billing

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

The minimum billable execution period for both execution modes is 1,000 ms. Past that, the billable activity period is rounded up to the nearest 100 ms. You can find details on the Flex Consumption plan billing meters in the [Monitoring reference](monitor-functions-reference?tab=flex-consumption-plan#metrics).

For details about how costs are calculated when you run in a Flex Consumption plan, including examples, see [Consumption-based costs](functions-consumption-costs?tabs=flex-consumption-plan#consumption-based-costs) and [Viewing cost-related data](functions-consumption-costs?tabs=flex-consumption-plan#viewing-and-estimating-costs-from-metrics).

## Supported language stack versions

This table shows the language stack versions that are currently supported for Flex Consumption apps:

| Language stack | Required version |
|---|---|
C# (isolated worker model)1 |
.NET 8, .NET 9, .NET 10 |
| Java | Java 11, Java 17, Java 21 |
| Node.js | Node.js 20, Node.js 22 |
| PowerShell | PowerShell 7.4 |
| Python | Python 3.10, Python 3.11, Python 3.12 |

- The
[C# in-process model](functions-dotnet-class-library)isn't supported. You instead need to[migrate your .NET project to the isolated worker model](migrate-dotnet-to-isolated-model).

## Regional subscription memory quotas

All Flex Consumption apps in a subscription and region share a compute quota, like a shared bucket of resources. This quota applies only to Flex Consumption apps — other hosting plans like Consumption, Premium, and Dedicated don't count against it. The quota limits how much total compute your Flex Consumption apps can use at the same time. If your apps try to exceed the quota, some executions and deployments might be delayed or fail, and scaling is throttled. However, you can still create new apps.

### Default quota

Each region in a subscription has a default quota of **250 cores** (equivalent to **512,000 MB**) for all Flex Consumption app instances combined. You can use any combination of instance sizes and counts, as long as the total cores stay under the quota.

To calculate the cores used, multiply the cores per instance by the number of instances:

| Instance size | Cores per instance | Formula |
|---|---|---|
| 512 MB | 0.25 | instances × 0.25 |
| 2,048 MB | 1 | instances × 1 |
| 4,096 MB | 2 | instances × 2 |

### Quota examples

Each of these scenarios reaches the 250 core quota limit. When the quota is reached, apps in the region stop scaling:

| Scenario | Calculation | Total cores |
|---|---|---|
| One 512-MB app at 1,000 instances | 1,000 × 0.25 | 250 |
| Two 512-MB apps at 250 and 750 instances | (250 + 750) × 0.25 | 250 |
| One 2,048-MB app at 250 instances | 250 × 1 | 250 |
| Two 2,048-MB apps at 100 and 150 instances | (100 + 150) × 1 | 250 |
| One 4,096-MB app at 125 instances | 125 × 2 | 250 |
| One 4,096-MB app at 100 instances + one 2,048-MB app at 50 instances | (100 × 2) + (50 × 1) | 250 |

### Important notes

- Flex Consumption scales rapidly based on
[concurrency](#concurrency)settings, so apps frequently acquire and release cores from the quota as demand changes. - Flex Consumption apps that scale to zero, or instances marked to be scaled in and deleted, don't count against the quota.
- Always ready instances count against quota.
- A
**Flex Consumption Quota tool**is available in the Azure portal. Open any Flex Consumption app in your subscription, select**Diagnose and solve problems**, search for`Flex Consumption Quota`

, then choose a region. The tool displays recommendations, current quota information, and historical usage views. - This quota can be increased pending capacity review. For example, from 250 cores to 1,000 cores or more. To request a larger quota, create a support ticket or contact your Microsoft account team.

## Deprecated properties and settings

In the Flex Consumption plan, many standard application settings and site configuration properties are deprecated or moved. Don't use these settings when you automate function app resource creation. For more information, see [Flex Consumption plan deprecations](functions-app-settings#flex-consumption-plan-deprecations).

## Considerations

Keep these other considerations in mind when using Flex Consumption plan:

**Apps per Plan**: Only one app is allowed per Flex Consumption plan.**Host**: There's a 30-second time-out for app initialization. When your function app takes longer than 30 seconds to start, you might see gRPC-related`System.TimeoutException`

entries logged. You can't currently configure this time-out. For more information, see[this host work item](https://github.com/Azure/azure-functions-host/issues/10482).**Durable Functions**: Azure Storage and Durable Task Scheduler are the only supported[storage providers](durable/durable-functions-storage-providers)for Durable Functions when hosted in the Flex Consumption plan. See[recommendations](durable/durable-functions-azure-storage-provider#flex-consumption-plan)when hosting Durable Functions in the Flex Consumption plan.**Virtual network integration and Resource provider registration**: You must have the`Microsoft.App`

Azure resource provider registered in your subscription to integrate to a virtual network, which is needed for subnet delegation. The Azure portal and Azure CLI enforce registration at app creation time since virtual network integration can be enabled at any point after your app is created. To register this provider,[follow these instructions](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider). The subnet delegation required by Flex Consumption apps is`Microsoft.App/environments`

.**Triggers**: While all triggers are fully supported in a Flex Consumption plan, the Blob storage trigger only supports the[Event Grid source](functions-event-grid-blob-trigger). Non-C# function apps must use version`[4.0.0, 5.0.0)`

of the[extension bundle](extension-bundles), or a later version.**Regions**: While the Flex Consumption plan is available in many Azure regions, not all regions are currently supported. To learn more, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Deployments**: Deployment slots aren't currently supported. For zero downtime deployments with Flex Consumption, see[Site update strategies in Flex Consumption](flex-consumption-site-updates).**Azure Storage as a local share**: Network File System (NFS) file shares aren't available for Flex Consumption. Only Server Message Block (SMB) and Azure Blobs (read-only) are supported.**Scale**: The lowest maximum scale is currently`40`

. The highest currently supported value is`1000`

.**PowerShell Managed dependencies**: Flex Consumption doesn't support[managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature). You must instead[upload modules with app content](functions-reference-powershell#including-modules-in-app-content).**Certificates**: Loading certificates with the WEBSITE_LOAD_CERTIFICATES app setting, managed certificates, app service certificates, and other platform certificate-based features like endToEndEncryptionEnabled are currently not supported.**Timezones**:`WEBSITE_TIME_ZONE`

and`TZ`

app settings aren't currently supported when running on Flex Consumption plan.**Azure Functions Runtime Version and Proxies**: Flex Consumption only supports version 4.x and later of the Azure Functions runtime. Azure Functions proxies was a feature of versions 1.x through 3.x of the Azure Functions runtime and is not available in Flex Consumption.

## Related articles

[Azure Functions hosting options](functions-scale)
[Create and manage function apps in the Flex Consumption plan](flex-consumption-how-to)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-develop-vs -->

# Develop Azure Functions using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Visual Studio provides a way to develop, test, and deploy C# class library functions to Azure. If this experience is your first with Azure Functions, see [Azure Functions overview](functions-overview).

To get started right away, consider completing the [Functions quickstart for Visual Studio](functions-create-your-first-function-visual-studio).

This article provides detailed information about how to use Visual Studio to develop C# class library functions and publish them to Azure.
There are two models for developing C# class library functions: the [isolated worker model](dotnet-isolated-process-guide) and the [in-process model](functions-dotnet-class-library).

You're reading the isolated worker model version of this article. You can select your preferred model at the top of the article.

You're reading the in-process model version of this article. You can select your preferred model at the top of the article.

Important

[Support for the in-process model ends on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We recommend that you [migrate your apps to the isolated worker model](migrate-dotnet-to-isolated-model).

Unless otherwise noted, procedures and examples shown are for Visual Studio 2022. For more information about Visual Studio 2022 releases, see the [release notes](/en-us/visualstudio/releases/2022/release-notes) or the [preview release notes](/en-us/visualstudio/releases/2022/release-notes-preview).

## Prerequisites

Visual Studio 2022, including the

**Azure development**workload.Other resources that you need, such as an Azure Storage account, are created in your subscription during the publishing process.

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Functions project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In the

**Create a new project**dialog, enter**functions**in the search box, select the**Azure Functions**template, and then select**Next**.In the

**Configure your new project**dialog, for**Project name**, enter a name for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.In the

**Additional information**dialog, take the actions listed in the following table:Setting Action Description **Functions worker**Select **.NET 8.0 Isolated (Long Term Support)**.Visual Studio creates a function project that runs in an [isolated worker process](dotnet-isolated-process-guide). The isolated worker process also supports other versions of .NET and .NET Framework that don't offer long term support (LTS). For more information, see[Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**.When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Setting Action Description **Functions worker**Select **.NET 8.0 In-process (Long Term Support)**.Visual Studio creates a function project that runs in-process with version 4.x of the Functions runtime. For more information, see [Azure Functions runtime versions overview](functions-versions).**Function**Select **Http trigger**.Visual Studio creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Select this checkbox. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use a Storage account connection string. All other trigger types require a valid Storage account connection string. **Authorization level**Select **Anonymous**When you use this authorization setting, any client can trigger the created function without providing a key. This configuration makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you select the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint.Select

**Create**to create the function project and HTTP trigger function.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.Azure.Functions.Worker`

and `Microsoft.Azure.Functions.Worker.Sdk`

NuGet packages, and sets the target framework.

After you create a Functions project, the project template creates a C# project, installs the `Microsoft.NET.Sdk.Functions`

NuGet package, and sets the target framework.

The new project has the following files:

*host.json*: This file provides a way for you to configure the Functions host. These settings apply both when running locally and in Azure. For more information, see[host.json reference](functions-host-json).*local.settings.json*: This file maintains settings that you use when you run functions locally. These settings aren't used when your app runs in Azure. For more information, see[Work with app settings locally](#local-settings).Important

Because the

*local.settings.json*file can contain secrets, you must exclude it from your project source control. In the**Properties**dialog for this file, make sure the**Copy to Output Directory**setting is set to**Copy if newer**.

For more information, see [Project structure](dotnet-isolated-process-guide#project-structure) in the isolated worker guide.

For more information, see [Functions class library project](functions-dotnet-class-library#functions-class-library-project).

## Work with app settings locally

When your function app runs in Azure, settings required by your functions are [stored encrypted in app settings](functions-how-to-use-azure-function-app-settings#settings). During local development, these settings are instead added to the `Values`

collection in the *local.settings.json* file. The *local.settings.json* file also stores settings used by local development tools.

Items in the `Values`

collection in your project's *local.settings.json* file are intended to mirror items in your function app's [application settings](functions-how-to-use-azure-function-app-settings#settings) in Azure.

Visual Studio doesn't automatically upload the settings in *local.settings.json* when you publish the project. To make sure that these settings also exist in your function app in Azure, upload them after you publish your project. For more information, see [Function app settings](#function-app-settings). The values in a `ConnectionStrings`

collection aren't published.

Your code can also read the function app settings values as environment variables. For more information, see [Environment variables](functions-dotnet-class-library#environment-variables).

## Configure the project for local development

The Functions runtime uses a Storage account internally. During development, you can use a valid Storage account for this internal account, or you can use the [Azurite emulator](../storage/common/storage-use-azurite).

For all trigger types other than HTTP and webhooks, you need to set the value of the `Values.AzureWebJobsStorage`

key in the *local.settings.json* file:

- For a Storage account, set the value to the connection string of your storage account.
- For the emulator, set the value to
`UseDevelopmentStorage=true`

.

If you use the emulator, change this setting to an actual storage account connection string before deployment. For more information, see [Local storage emulator](functions-develop-local#local-storage-emulator).

To set the storage account connection string, take the following steps:

Sign in to the

[Azure portal](https://portal.azure.com), and then go to your storage account.Select

**Security + networking**>**Access keys**. Under**key1**, copy the**Connection string**value.In your Visual Studio project, open the

*local.settings.json*file. Set the value of the`AzureWebJobsStorage`

key to the connection string you copied.Repeat the previous step to add unique keys to the

`Values`

array for any other connections required by your functions.

## Add a function to your project

In C# class library functions, the bindings that the functions use are defined by applying attributes in the code. When you create your function triggers from the provided templates, the trigger attributes are applied for you.

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.In the

**Add New Item**dialog, select**Azure Function**, and then select**Add**.Select a trigger, and then set the required binding properties. If you select a Storage service trigger and you want to configure the connection, select the checkbox for configuring the trigger connection. The following example shows the settings for creating a Queue Storage trigger function.

Select

**Add**. If you select the checkbox for configuring a storage connection in the previous step, the**Connect to dependency**page appears. Select an Azurite storage emulator or**Azure Storage**, and then select**Next**.- If you select an Azurite storage emulator, the
**Connect to Storage Azurite emulator**page appears. Take the following steps:- Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select
- If you select
**Azure Storage**, the**Connect to Azure Storage**page appears. Take the following steps:- Select a storage account, and then select
**Next**. Visual Studio tries to connect to your Azure account and retrieve an endpoint. - Select
**Next**. - On the
**Summary of changes**page, select**Finish**. Visual Studio configures the dependency and creates the trigger class.

- Select a storage account, and then select

This trigger example uses an application setting for the storage connection with a key named

`QueueStorage`

. This key, stored in the[local.settings.json file](functions-develop-local#local-settings-file), either references the Azurite emulator or a Storage account.- If you select an Azurite storage emulator, the
Examine the newly added class. For example, the following C# class represents a basic Queue Storage trigger function:

A

`Run()`

method is attributed with`Function`

. This attribute indicates that the method is the entry point for the function.`using System; using Azure.Storage.Queues.Models; using Microsoft.Azure.Functions.Worker; using Microsoft.Extensions.Logging; namespace Company.Function; public class QueueTriggerCSharp { private readonly ILogger<QueueTriggerCSharp> _logger; public QueueTriggerCSharp(ILogger<QueueTriggerCSharp> logger) { _logger = logger; } [Function(nameof(QueueTriggerCSharp))] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")] QueueMessage message) { _logger.LogInformation("C# Queue trigger function processed: {messageText}", message.MessageText); } }`

A static

`Run()`

method is attributed with`FunctionName`

. This attribute indicates that the method is the entry point for the function.`using System; using Microsoft.Azure.WebJobs; using Microsoft.Azure.WebJobs.Host; using Microsoft.Extensions.Logging; namespace Company.Function { public class QueueTriggerCSharp { [FunctionName("QueueTriggerCSharp")] public void Run([QueueTrigger("PathValue", Connection = "ConnectionValue")]string myQueueItem, ILogger log) { log.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); } } }`


A binding-specific attribute is applied to each binding parameter supplied to the entry point method. The attribute takes the binding information as parameters.

In the preceding code, the first parameter has a `QueueTrigger`

attribute applied, which indicates a Queue Storage trigger function. The queue name and connection string setting name are passed as parameters to the `QueueTrigger`

attribute. In your class:

- The queue name parameter should match the name of the queue you use in an earlier step to create the trigger, such as
`myqueue-items`

. - The connection string setting name should match the one you use in an earlier step to create the trigger, such as
`QueueStorage`

.

For more information, see [Azure Queue storage trigger for Azure Functions](functions-bindings-storage-queue-trigger).

Use the preceding procedure to add more functions to your function app project. Each function in the project can have a different trigger, but a function must have exactly one trigger. For more information, see [Azure Functions triggers and bindings](functions-triggers-bindings).

## Add bindings

As with triggers, input and output bindings are added to your function as binding attributes. To add bindings to a function, take the following steps:

Make sure you

[configure the project for local development](#configure-the-project-for-local-development).Add the appropriate NuGet extension package for each specific binding. For binding-specific NuGet package requirements, see the reference article for the binding. For example, for package requirements for the Azure Event Hubs trigger, see

[Azure Event Hubs trigger and bindings for Azure Functions](functions-bindings-event-hubs).Use the following command in the Package Manager Console to install a specific package:

`Install-Package Microsoft.Azure.Functions.Worker.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

`Install-Package Microsoft.Azure.WebJobs.Extensions.<BINDING_TYPE> -Version <TARGET_VERSION>`

In this code, replace

`<BINDING_TYPE>`

with the specific name of the binding extension, and replace`<TARGET_VERSION>`

with a specific version of the package, such as`4.0.0`

. Valid versions are listed on the individual package pages at[NuGet.org](https://nuget.org).If there are app settings that the binding needs, add them to the

`Values`

collection in the[local setting file](functions-develop-local#local-settings-file).The function uses these values when it runs locally. When the function runs in the function app in Azure, it uses the

[function app settings](#function-app-settings). Visual Studio makes it easy to[publish local settings to Azure](#function-app-settings).Add the appropriate binding attribute to the method signature. In the following code, a queue message triggers the

`Run`

function. The output binding then creates a new queue message with the same text in a different queue.`public class QueueTrigger { private readonly ILogger _logger; public QueueTrigger(ILoggerFactory loggerFactory) { _logger = loggerFactory.CreateLogger<QueueTrigger>(); } [Function("CopyQueueMessage")] [QueueOutput("myqueue-items-destination", Connection = "QueueStorage")] public string Run([QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem) { _logger.LogInformation($"C# Queue trigger function processed: {myQueueItem}"); return myQueueItem; } }`

The

`QueueOutput`

attribute defines the binding on the method. For multiple output bindings, you instead place this attribute on a string property of the returned object. For more information, see[Multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings).`public static class SimpleExampleWithOutput { [FunctionName("CopyQueueMessage")] public static void Run( [QueueTrigger("myqueue-items-source", Connection = "QueueStorage")] string myQueueItem, [Queue("myqueue-items-destination", Connection = "QueueStorage")] out string myQueueItemCopy, ILogger log) { log.LogInformation($"CopyQueueMessage function processed: {myQueueItem}"); myQueueItemCopy = myQueueItem; } }`

The

`Queue`

attribute on the`out`

parameter defines the output binding.The connection to Queue Storage is obtained from the

`QueueStorage`

setting. For more information, see the reference article for the specific binding.

For a full list of the bindings supported by Functions, see [Supported bindings](functions-triggers-bindings?tabs=csharp#supported-bindings). For a more complete example of this scenario, see [Connect functions to Azure Storage using Visual Studio](functions-add-output-binding-storage-queue-vs).

## Run functions locally

You can use Azure Functions Core Tools to run Functions projects on your local development computer. When you select **F5** to debug a Functions project, the local Functions host (`func.exe`

) starts to listen on a local port (usually 7071). Any callable function endpoints are written to the output, and you can use these endpoints for testing your functions. For more information, see [Develop Azure Functions locally using Core Tools](functions-run-local). You're prompted to install these tools the first time you start a function from Visual Studio.

Important

Starting with version 4.0.6517 of the Core Tools, in-process model projects must reference [version 4.5.0 or later of Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/4.5.0). If you use an earlier version, the

`func start`

command generates an error.To start your function in Visual Studio in debug mode, take the following steps:

Select

**F5**. If prompted, accept the request from Visual Studio to download and install Azure Functions Core Tools. You might also need to turn on a firewall exception so that the tools can handle HTTP requests.When the project runs, test your code the same way you test a deployed function.

When you run Visual Studio in debug mode, breakpoints are hit as expected.


For a more detailed testing scenario that uses Visual Studio, see [Test functions](#test-functions), later in this article.

## Publish to Azure

When you publish your Functions project to Azure, Visual Studio uses [zip deployment](functions-deployment-technologies#zip-deploy) to deploy the project files. When possible, you should also select **Run from package file** so that the project runs in the deployment (.zip) package. For more information, see [Run your functions from a package file in Azure](run-functions-from-deployment-package).

Don't deploy to Functions by using Web Deploy (`msdeploy`

).

Use the following steps to publish your project to a function app in Azure:

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).[Application Insights](functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Function app settings

Visual Studio doesn't upload app settings automatically when you publish your project. If you add settings to the *local.settings.json* file, you must also add them to the function app in Azure.

The easiest way to upload the required settings to your function app in Azure is to manage them in Visual Studio. On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Manage Azure App Service settings**.

When you make the selection, the **Application settings** dialog opens for the function app. You can use this dialog to add application settings or modify existing ones.


For each setting, the **Local** value is the value in the *local.settings.json* file, and the **Remote** value is the value in the function app in Azure.

- To create an app setting, select
**Add setting**. - To copy a setting value from the
**Local**field to the**Remote**field, select**Insert value from Local**.

Pending changes are written to the local settings file and the function app when you select **OK**.

Note

By default, the *local.settings.json* file isn't checked into source control. As a result, if you clone a local Functions project from source control, the project doesn't have a *local.settings.json* file. You need to manually create the *local.settings.json* file in the project root so that the **Application settings** dialog works as expected.

You can also manage application settings in one of these other ways:

- Use the
[Azure portal](functions-how-to-use-azure-function-app-settings#settings). - Use the
.`--publish-local-settings`

publish option in the Azure Functions Core Tools - Use the
[Azure CLI](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-set).

## Remote debugging

To debug your function app remotely, you must publish a debug configuration of your project. You also need to turn on remote debugging in your function app in Azure.

This section assumes a debug configuration to your function app is published.

### Remote debugging considerations

- Remote debugging isn't recommended on a production service.
- To use remote debugging, you must host your function app in a Premium or App Service plan.
- Remote debugging is currently only supported when running your C# app on Windows.
- If you have the Just My Code feature turned on in Visual Studio, turn it off. For instructions, see
[Enable or disable Just My Code](/en-us/visualstudio/debugger/just-my-code#BKMK_Enable_or_disable_Just_My_Code). - Avoid long stops at breakpoints when you use remote debugging. When a process is stopped for longer than a few minutes, Azure treats it as an unresponsive process and shuts it down.
- While you're debugging, the server sends data to Visual Studio, which can affect bandwidth charges. For information about bandwidth rates, see
[Pricing calculator](https://azure.microsoft.com/pricing/calculator/). - Remote debugging is automatically turned off in your function app after 48 hours. After that point, you need to turn remote debugging back on.

### Attach the debugger

When you debug an isolated worker process app, you currently need to attach the remote debugger to a separate .NET process. Several other configuration steps are also required.

To attach a remote debugger to a function app running in a process separate from the Functions host, take the following steps:

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Attach debugger**.Visual Studio connects to your function app and turns on remote debugging if it's not already turned on.

Note

Because the remote debugger can't connect to the host process, an error message might appear. In any case, the local debugger can't access your breakpoints or provide a way for you to inspect variables or step through code.

On the Visual Studio

**Debug**menu, select**Attach to Process**.In the

**Attach to Process**dialog, take the following steps:- Next to
**Connection type**, select**Microsoft Azure App Services**. - Next to
**Connection target**, select**Find**.

- Next to
In the

**Azure Attach to Process**dialog, search for and select your function app, and then select**OK**.If prompted, allow Visual Studio access through your local firewall.

Back in the

**Attach to Process**dialog, select**Show processes for all users**. Select**dotnet.exe**, and then select**Attach**.

When the operation finishes, you're attached to your C# class library code running in an isolated worker process. At this point, you can debug your function app as normal.

To attach a remote debugger to a function app running in-process with the Functions host, take the following steps.

On the publish profile page, go to the **Hosting** section. Select the ellipsis (**...**), and then select **Attach debugger**.

Visual Studio connects to your function app and turns on remote debugging if it's not already turned on. It also locates and attaches the debugger to the host process for the app. At this point, you can debug your function app as normal.

When you finish debugging, you should [turn off remote debugging](#turn-off-remote-debugging).

### Turn off remote debugging

After you finish remote debugging your code, you should turn off remote debugging in the [Azure portal](https://portal.azure.com). Remote debugging is automatically turned off after 48 hours, in case you forget.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The Azure portal opens to the function app your project is deployed to.In the function app, select

**Settings**>**Configuration**, and then go to the**General settings**tab. Next to**Remote debugging**, select**Off**. Select**Save**, and then select**Continue**.

After the function app restarts, you can no longer remotely connect to your remote processes. You can use this same tab in the Azure portal to turn on remote debugging outside of Visual Studio.

## Monitor functions

The recommended way to monitor your functions is by integrating your function app with Application Insights. You should turn on this integration when you create your function app during Visual Studio publishing.

If the integration isn't set up during publishing for some reason, you should still turn on [Application Insights integration](configure-monitoring#enable-application-insights-integration) for your function app in Azure.

For more information about using Application Insights for monitoring, see [Monitor executions in Azure Functions](functions-monitoring).

## Test functions

This section describes how to create a C# in-process model project that you can test by using [xUnit](https://github.com/xunit/xunit), an open-source unit testing tool for .NET.

### Step 1: Setup

Follow these steps to configure the environment, including the app project and functions, required to support your tests:

In Visual Studio, create an Azure Functions project named

**Functions**.Create an HTTP function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Http trigger**, and then select**Add**. - Rename the new class
*MyHttpTrigger*.

- In
Create a timer function from the template:

- In
**Solution Explorer**, right-click the**Functions**project, and then select**Add**>**New Azure Function**. - In the
**Add New Item**dialog, select**Azure Function**, and then select**Add**. - Select
**Timer trigger**, and then select**Add**. - Rename the new class
*MyTimerTrigger*.

- In
Create an

[xUnit Test app](https://xunit.net/docs/getting-started/v3/getting-started)in the solution:- In
**Solution Explorer**, right-click the solution that contains your**Functions**project, and then select**Add**>**New Project**. - Select the
**xUnit Test Project**template, and then select**Next**. - Name the project
**Functions.Tests**.

- In
Remove the default test files from the

**Functions.Tests**project.Use NuGet to add a reference from the test app to

[Microsoft.AspNetCore.Mvc](https://www.nuget.org/packages/Microsoft.AspNetCore.Mvc/). You can use Package Manager Console, or you can take the following steps:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Manage NuGet Packages**. - Search for and install
**Microsoft.AspNetCore.Mvc**.

- In
In the

**Functions.Tests**app,[add a reference](/en-us/visualstudio/ide/managing-references-in-a-project)to the**Functions**app:- In
**Solution Explorer**, right-click the**Functions.Tests**project, and then select**Add**>**Project Reference**. - Select the
**Functions**project, and then select**OK**.

- In

### Step 2: Create test classes

In this section, you create the classes that you use to run the automated tests.

Each function takes an implementation of [ ILogger](/en-us/dotnet/api/microsoft.extensions.logging.ilogger) to handle message logging. In some tests, no messages are logged, or it doesn't matter how logging is implemented. Other tests need to evaluate logged messages to determine whether a test should pass.

Create a class in your

**Functions.Tests**project named`NullScope`

and add the following code. This class provides a mock scope. In a later step, you create an implementation of`ILogger`

that uses this scope.`using System; namespace Functions.Tests { public class NullScope : IDisposable { public static NullScope Instance { get; } = new NullScope(); private NullScope() { } public void Dispose() { } } }`

Create a class in your

**Functions.Tests**project named`ListLogger`

and add the following code. This class maintains an internal list of messages to evaluate during testing. To implement the required`ILogger`

interface, the class uses the mock scope from the`NullScope`

class. The test cases pass the mock scope to the`ListLogger`

class.`using Microsoft.Extensions.Logging; using System; using System.Collections.Generic; using System.Text; namespace Functions.Tests { public class ListLogger : ILogger { public IList<string> Logs; public IDisposable BeginScope<TState>(TState state) => NullScope.Instance; public bool IsEnabled(LogLevel logLevel) => false; public ListLogger() { this.Logs = new List<string>(); } public void Log<TState>(LogLevel logLevel, EventId eventId, TState state, Exception exception, Func<TState, Exception, string> formatter) { string message = formatter(state, exception); this.Logs.Add(message); } } }`

The

`ListLogger`

class implements the following members, as contracted by the`ILogger`

interface:`BeginScope`

: Scopes add context to your logging. In this case, the test points to the static instance on the`NullScope`

class to allow the test to function.`IsEnabled`

: A default value of`false`

is provided.`Log`

: This method uses the provided`formatter`

function to format the message. The method then adds the resulting text to the`Logs`

collection.

The

`Logs`

collection is an instance of`List<string>`

and is initialized in the constructor.Create a code file in the

**Functions.Tests**project named*LoggerTypes.cs*and add the following code:`namespace Functions.Tests { public enum LoggerTypes { Null, List } }`

This enumeration specifies the type of logger that the tests use.

Create a class in the

**Functions.Tests**project named`TestFactory`

and add the following code:`using Microsoft.AspNetCore.Http; using Microsoft.AspNetCore.Http.Internal; using Microsoft.Extensions.Logging; using Microsoft.Extensions.Logging.Abstractions; using Microsoft.Extensions.Primitives; using System.Collections.Generic; namespace Functions.Tests { public class TestFactory { public static IEnumerable<object[]> Data() { return new List<object[]> { new object[] { "name", "Bernardo" }, new object[] { "name", "Ananya" }, new object[] { "name", "Vlad" } }; } private static Dictionary<string, StringValues> CreateDictionary(string key, string value) { var qs = new Dictionary<string, StringValues> { { key, value } }; return qs; } public static HttpRequest CreateHttpRequest(string queryStringKey, string queryStringValue) { var context = new DefaultHttpContext(); var request = context.Request; request.Query = new QueryCollection(CreateDictionary(queryStringKey, queryStringValue)); return request; } public static ILogger CreateLogger(LoggerTypes type = LoggerTypes.Null) { ILogger logger; if (type == LoggerTypes.List) { logger = new ListLogger(); } else { logger = NullLoggerFactory.Instance.CreateLogger("Null Logger"); } return logger; } } }`

The

`TestFactory`

class implements the following members:`Data`

: This property returns an[IEnumerable](/en-us/dotnet/api/system.collections.ienumerable)collection of sample data. The key-value pairs represent values that are passed into a query string.`CreateDictionary`

: This method accepts a key-value pair as an argument. It returns a new instance of`Dictionary`

that's used to create an instance of`QueryCollection`

to represent query string values.`CreateHttpRequest`

: This method creates an HTTP request that's initialized with the given query string parameters.`CreateLogger`

: This method returns an implementation of`ILogger`

that's used for testing. The`ILogger`

implementation depends on the specified logger type. If a list type is specified, the`ListLogger`

instance keeps track of logged messages that are available for evaluation in tests.

Create a class in the

**Functions.Tests**project named`FunctionsTests`

and add the following code:`using Microsoft.AspNetCore.Mvc; using Microsoft.Extensions.Logging; using Xunit; namespace Functions.Tests { public class FunctionsTests { private readonly ILogger logger = TestFactory.CreateLogger(); [Fact] public async void Http_trigger_should_return_known_string() { var request = TestFactory.CreateHttpRequest("name", "Bernardo"); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal("Hello, Bernardo. This HTTP triggered function executed successfully.", response.Value); } [Theory] [MemberData(nameof(TestFactory.Data), MemberType = typeof(TestFactory))] public async void Http_trigger_should_return_known_string_from_member_data(string queryStringKey, string queryStringValue) { var request = TestFactory.CreateHttpRequest(queryStringKey, queryStringValue); var response = (OkObjectResult)await MyHttpTrigger.Run(request, logger); Assert.Equal($"Hello, {queryStringValue}. This HTTP triggered function executed successfully.", response.Value); } [Fact] public void Timer_should_log_message() { var logger = (ListLogger)TestFactory.CreateLogger(LoggerTypes.List); new MyTimerTrigger().Run(null, logger); var msg = logger.Logs[0]; Assert.Contains("C# Timer trigger function executed at", msg); } } }`

This class implements the following members:

`Http_trigger_should_return_known_string`

: This test uses the query string value`name=Bernardo`

to create a request to an HTTP function. This test checks that the expected response is returned.`Http_trigger_should_return_string_from_member_data`

: This test uses xUnit attributes to provide sample data to the HTTP function.`Timer_should_log_message`

: This test creates an instance of`ListLogger`

and passes it to a timer function. After the function runs, the log is checked to make sure the expected message is present.

To access application settings in your tests, you can

[inject](functions-dotnet-dependency-injection)an`IConfiguration`

implementation with mocked environment variable values into your function.

### Step 3: Run tests

To run the tests in Visual Studio, select **View** > **Test Explorer**. In **Test Explorer**, select **Run** > **Run All Tests in View**.


### Step 4: Debug tests

To debug the tests, set a breakpoint on a test. In **Test Explorer**, select **Run** > **Debug Last Run**.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-iot-trigger -->

# Azure IoT Hub trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with Azure Functions bindings for IoT Hub. The IoT Hub support is based on the [Azure Event Hubs Binding](functions-bindings-event-hubs).

For information on setup and configuration details, see the [overview](functions-bindings-event-iot).

Important

While the following code samples use the Event Hub API, the given syntax is applicable for IoT Hub functions.

Use the function trigger to respond to an event sent to an event hub event stream. You need read access to the underlying event hub to set up the trigger. When the function is triggered, the message passed to the function is typed as a string.

Event Hubs scaling decisions for the Consumption and Premium plans are done via Target Based Scaling. For more information, see [Target Based Scaling](functions-target-based-scaling).

For information about how Azure Functions responds to events sent to an event hub event stream using triggers, see [Integrate Event Hubs with serverless functions on Azure](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

The following example shows a [C# function](dotnet-isolated-process-guide) that is triggered based on an event hub, where the input message string is written to the logs:

```
{
private readonly ILogger<EventHubsFunction> _logger;
public EventHubsFunction(ILogger<EventHubsFunction> logger)
{
_logger = logger;
}
[Function(nameof(EventHubFunction))]
[FixedDelayRetry(5, "00:00:10")]
[EventHubOutput("dest", Connection = "EventHubConnection")]
public string EventHubFunction(
[EventHubTrigger("src", Connection = "EventHubConnection")] string[] input,
FunctionContext context)
{
_logger.LogInformation("First Event Hubs triggered message: {msg}", input[0]);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following example shows an Event Hubs trigger [TypeScript function](functions-reference-node?tabs=typescript). The function reads [event metadata](#event-metadata) and logs the message.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(message: unknown, context: InvocationContext): Promise<void> {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: eventHubTrigger1,
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
import { app, InvocationContext } from '@azure/functions';
export async function eventHubTrigger1(messages: unknown[], context: InvocationContext): Promise<void> {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
}
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: eventHubTrigger1,
});
```


The following example shows an Event Hubs trigger [JavaScript function](functions-reference-node). The function reads [event metadata](#event-metadata) and logs the message.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'one',
handler: (message, context) => {
context.log('Event hub function processed message:', message);
context.log('EnqueuedTimeUtc =', context.triggerMetadata.enqueuedTimeUtc);
context.log('SequenceNumber =', context.triggerMetadata.sequenceNumber);
context.log('Offset =', context.triggerMetadata.offset);
},
});
```


To receive events in a batch, set `cardinality`

to `many`

, as shown in the following example.

```
const { app } = require('@azure/functions');
app.eventHub('eventHubTrigger1', {
connection: 'myEventHubReadConnectionAppSetting',
eventHubName: 'MyEventHub',
cardinality: 'many',
handler: (messages, context) => {
context.log(`Event hub function processed ${messages.length} messages`);
for (let i = 0; i < messages.length; i++) {
context.log('Event hub message:', messages[i]);
context.log(`EnqueuedTimeUtc = ${context.triggerMetadata.enqueuedTimeUtcArray[i]}`);
context.log(`SequenceNumber = ${context.triggerMetadata.sequenceNumberArray[i]}`);
context.log(`Offset = ${context.triggerMetadata.offsetArray[i]}`);
}
},
});
```


Here's the PowerShell code:

```
param($eventHubMessages, $TriggerMetadata)
Write-Host "PowerShell eventhub trigger function called for message array: $eventHubMessages"
$eventHubMessages | ForEach-Object { Write-Host "Processed message: $_" }
```


This example uses SDK types to directly access the underlying [ EventData](/en-us/python/api/azure-eventhub/azure.eventhub.eventdata) object provided by the Event Hubs trigger:

The function reads the event body and logs it.

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.eventhub as eh
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.event_hub_message_trigger(
arg_name="event", event_hub_name="EVENTHUB_NAME", connection="EventHubConnection"
)
def eventhub_trigger(event: eh.EventData):
logging.info(
"Python EventHub trigger processed an event %s",
event.body_as_str()
)
```


For examples of using the EventData type, see the [ EventData](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-eventhub/samples/eventhub_samples_eventdata/function_app.py) samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the

[Python SDK Bindings for Event Hubs Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python).

Note

Known limitations include:

- The
`enqueued_time`

property is not supported. - Batch message support is supported with runtime version 4.1039 or greater.

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

The following example shows an Event Hubs trigger binding and a Python function that uses the binding. The function reads [event metadata](#event-metadata) and logs the message. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="EventHubTrigger1")
@app.event_hub_message_trigger(arg_name="myhub",
event_hub_name="<EVENT_HUB_NAME>",
connection="<CONNECTION_SETTING>")
def test_function(myhub: func.EventHubEvent):
logging.info('Python EventHub trigger processed an event: %s',
myhub.get_body().decode('utf-8'))
```


The following example shows an Event Hubs trigger binding which logs the message body of the Event Hubs trigger.

```
@FunctionName("ehprocessor")
public void eventHubProcessor(
@EventHubTrigger(name = "msg",
eventHubName = "myeventhubname",
connection = "myconnvarname") String message,
final ExecutionContext context )
{
context.getLogger().info(message);
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `EventHubTrigger`

annotation on parameters whose value comes from the event hub. Parameters with these annotations cause the function to run when an event arrives. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

The following example illustrates extensive use of `SystemProperties`

and other Binding options for further introspection of the Event along with providing a well-formed `BlobOutput`

path that is Date hierarchical.

```
package com.example;
import java.util.Map;
import java.time.ZonedDateTime;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
/**
* Azure Functions with Event Hub trigger.
* and Blob Output using date in path along with message partition ID
* and message sequence number from EventHub Trigger Properties
*/
public class EventHubReceiver {
@FunctionName("EventHubReceiver")
@StorageAccount("bloboutput")
public void run(
@EventHubTrigger(name = "message",
eventHubName = "%eventhub%",
consumerGroup = "%consumergroup%",
connection = "eventhubconnection",
cardinality = Cardinality.ONE)
String message,
final ExecutionContext context,
@BindingName("Properties") Map<String, Object> properties,
@BindingName("SystemProperties") Map<String, Object> systemProperties,
@BindingName("PartitionContext") Map<String, Object> partitionContext,
@BindingName("EnqueuedTimeUtc") Object enqueuedTimeUtc,
@BlobOutput(
name = "outputItem",
path = "iotevents/{datetime:yy}/{datetime:MM}/{datetime:dd}/{datetime:HH}/" +
"{datetime:mm}/{PartitionContext.PartitionId}/{SystemProperties.SequenceNumber}.json")
OutputBinding<String> outputItem) {
var et = ZonedDateTime.parse(enqueuedTimeUtc + "Z"); // needed as the UTC time presented does not have a TZ
// indicator
context.getLogger().info("Event hub message received: " + message + ", properties: " + properties);
context.getLogger().info("Properties: " + properties);
context.getLogger().info("System Properties: " + systemProperties);
context.getLogger().info("partitionContext: " + partitionContext);
context.getLogger().info("EnqueuedTimeUtc: " + et);
outputItem.setValue(message);
}
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to configure the trigger. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#event-hubs-trigger).

Use the `EventHubTriggerAttribute`

to define a trigger on an event hub, which supports the following properties.

| Parameters | Description |
|---|---|
EventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced in
`%eventHubName%` |

**ConsumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. When omitted, the`$Default`

consumer group is used.**Connection**[Connections](#connections).## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `event_hub_message_trigger`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the event item in function code. |
`event_hub_name` |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Event Hubs. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) annotation, which supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.eventHub()`

method.

| Property | Description |
|---|---|
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).The following table explains the trigger configuration properties that you set in the *function.json* file, which differs by runtime version.

| function.json property | Description |
|---|---|
type |
Must be set to `eventHubTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the event item in function code. |
eventHubName |
The name of the event hub. When the event hub name is also present in the connection string, that value overrides this property at runtime. Can be referenced via
`%eventHubName%` |

**consumerGroup**[consumer group](../event-hubs/event-hubs-features#event-consumers)used to subscribe to events in the hub. If omitted, the`$Default`

consumer group is used.**cardinality**`many`

in order to enable batching. If omitted or set to `one`

, a single message is passed to the function.**connection**[Connections](#connections).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

To learn more about how Event Hubs trigger and IoT Hub trigger scales, see [Consuming Events with Azure Functions](/en-us/azure/architecture/serverless/event-hubs-functions/event-hubs-functions#consuming-events-with-azure-functions).

Functions also supports Python SDK type bindings for Azure Event Hubs, which lets you work with data using these underlying SDK types:

Important

Support for Event Hubs SDK types in Python is in Preview and is only supported for the Python v2 programming model. For more information, see [SDK types in Python](functions-reference-python#sdk-type-bindings).

The parameter type supported by the Event Hubs output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

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

The parameter type can be one of the following:

- Any native Java types such as int, String, byte[].
- Nullable values using Optional.
- Any POJO type.

To learn more, see the [EventHubTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.eventhubtrigger) reference.

## Event metadata

The Event Hubs trigger provides several [metadata properties](functions-bindings-expressions-patterns). Metadata properties can be used as part of binding expressions in other bindings or as parameters in your code. The properties come from the [EventData](/en-us/dotnet/api/microsoft.servicebus.messaging.eventdata) class.

| Property | Type | Description |
|---|---|---|
`PartitionContext` |
|

`PartitionContext`

instance.`EnqueuedTimeUtc`

`DateTime`

`Offset`

`string`

`PartitionKey`

`string`

`Properties`

`IDictionary<String,Object>`

`SequenceNumber`

`Int64`

`SystemProperties`

`IDictionary<String,Object>`

See [code examples](#example) that use these properties earlier in this article.

## Connections

The `connection`

property is a reference to environment configuration that contains name of an application setting containing a connection string. You can get this connection string by selecting the **Connection Information** button for the [namespace](../event-hubs/event-hubs-create#create-an-event-hubs-namespace). The connection string must be for an Event Hubs namespace, not the event hub itself.

The connection string must have at least "read" permissions to activate the function.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

Note

Identity-based connections aren't supported by the IoT Hub trigger. If you need to use managed identities end-to-end, you can instead use IoT Hub Routing to send data to an event hub you control. In that way, outbound routing can be authenticated with managed identity the event can be read [from that event hub using managed identity](functions-bindings-event-hubs-trigger?tabs=extensionv5#identity-based-connections).

## host.json properties

The [host.json](functions-host-json#eventhub) file contains settings that control Event Hub trigger behavior. See the [host.json settings](functions-bindings-event-iot#hostjson-settings) section for details regarding available settings.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-plan -->

# Azure Functions Flex Consumption plan hosting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Flex Consumption is a Linux-based Azure Functions hosting plan that builds on the Consumption *pay for what you use* serverless billing model. It gives you more flexibility and customizability by introducing private networking, instance memory size selection, and fast/large scale-out features still based on a *serverless* model.

You can review end-to-end samples that feature the Flex Consumption plan in the [Flex Consumption plan samples repository](https://github.com/Azure-Samples/azure-functions-flex-consumption-samples).

## Benefits

The Flex Consumption plan builds on the strengths of the serverless Consumption plan, which include dynamic scaling and execution-based billing. With Flex Consumption, you also get these extra features:

**Reduced Cold Start Times**: Enable[always-ready instances](#always-ready-instances)to achieve faster cold-start times compared to the Consumption plan.**Virtual network support**:[Virtual network integration](#virtual-network-integration)enables your serverless app to run in a virtual network.**Per-Function Scaling**: Each function in your app[scales independently based on its workload](#per-function-scaling), potentially resulting in more efficient resource allocation.**Improved Concurrency Handling**: Better handling of concurrent executions with configurable concurrency settings per function.**Flexible Memory Configuration**: Flex Consumption offers multiple[instance sizes](#instance-sizes)size options, allowing you to optimize for your specific workload requirements.

This table helps you directly compare the features of Flex Consumption with the Consumption hosting plan:

| Feature | Consumption | Flex Consumption |
|---|---|---|
| Scale to zero | ✅ Yes | ✅ Yes |
| Scale behavior |
|

[Event driven](event-driven-scaling)(fast)For a complete comparison of the Flex Consumption plan against the Consumption plan and all other plan and hosting types, see [function scale and hosting options](functions-scale).

Tip

If you're migrating from the Linux Consumption plan, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex?pivots=platform-linux) for step-by-step migration instructions and important differences between the plans.

## Virtual network integration

Flex Consumption expands on the traditional benefits of Consumption plan by adding support for [virtual network integration](functions-networking-options#virtual-network-integration). When your apps run in a Flex Consumption plan, they can connect to other Azure services secured inside a virtual network. All while still allowing you to take advantage of serverless billing and scale, together with the scale and throughput benefits of the Flex Consumption plan. For more information, see [Enable virtual network integration](flex-consumption-how-to#enable-virtual-network-integration).

## Instance sizes

When you create your function app in a Flex Consumption plan, you can select the memory size of the instances on which your app runs. See [Billing](#billing) to learn how instance memory sizes affect the costs of your function app.

Currently, Flex Consumption offers these instance size options:

| Instance Memory (MB) | CPU Cores |
|---|---|
| 512 | 0.25 |
| 2048 | 1 |
| 4096 | 2 |

Note

The CPU core values shown are typical allocations for instances with the specified memory size. However, initial instances might be granted slightly different core allocations to improve performance. Each Flex Consumption instance also includes an extra 272 MB of memory allocated by the platform as a buffer for system and host processes. This extra memory doesn't affect billing, and instances are billed based on the configured instance memory size shown in the preceding table.

When deciding on which instance memory size to use with your apps, here are some things to consider:

- The 2,048-MB instance memory size is the default and should be used for most scenarios. The 512 MB and 4,096-MB instance memory sizes are available for scenarios that best suit your application's concurrency or processing power requirements. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - You can change the instance memory size at any time. For more information, see
[Configure instance memory](flex-consumption-how-to#configure-instance-memory). - Instance resources are shared between your function code and the Functions host.
- The larger the instance memory size, the more each instance can handle as far as concurrent executions or more intensive CPU or memory workloads. Specific scale decisions are workload-specific.
- The default concurrency of HTTP triggers depends on the instance memory size. For more information, see
[HTTP trigger concurrency](functions-concurrency#http-trigger-concurrency). - Available CPUs and network bandwidth are provided proportional to a specific instance size.

## Per-function scaling

[Concurrency](#concurrency) is a key factor that determines how Flex Consumption function apps scale. To improve the scale performance of apps with various trigger types, the Flex Consumption plan provides a more deterministic way of scaling your app on a per-function basis.

This *per-function scaling* behavior is a part of the hosting platform, so you don't need to configure your app or change the code. For more information, see [Per-function scaling](event-driven-scaling#per-function-scaling) in the Event-driven scaling article.

In per-function scaling, decisions are made for certain function triggers based on group aggregations. This table shows the defined set of function scale groups:

| Scale groups | Triggers in group | Settings value |
|---|---|---|
| HTTP triggers |
|

`http`

(Event Grid-based)

[Blob storage trigger](functions-bindings-storage-blob-trigger)`blob`

[Orchestration trigger](durable/durable-functions-bindings#orchestration-trigger)[Activity trigger](durable/durable-functions-bindings#activity-trigger)[Entity trigger](durable/durable-functions-bindings#entity-trigger)`durable`

All other functions in the app are scaled individually in their own set of instances, which are referenced using the convention `function:<NAMED_FUNCTION>`

.

## Always ready instances

Flex Consumption includes an *always ready* feature that lets you choose instances that are always running and assigned to each of your per-function scale groups or functions. Always ready is a great option for scenarios where you need to have a minimum number of instances always ready to handle requests. For example, to reduce your application's cold start latency. The default is 0 (zero).

For example, if you set always ready to 2 for your HTTP group of functions, the platform keeps two instances always running for those functions. Those instances process your function executions first. Depending on concurrency settings, the platform scales beyond those two instances with on-demand instances.

No less than two always-ready instances can be configured per function or function group while [zone redundancy is enabled](/en-us/azure/reliability/reliability-functions?pivots=flex-consumption-plan#availability-zone-support).

To learn how to configure always ready instances, see [Set always ready instance counts](flex-consumption-how-to#set-always-ready-instance-counts).

## Concurrency

Concurrency refers to the number of parallel executions of a function on an instance of your app. You can set a maximum number of concurrent executions that each instance should handle at any given time. Concurrency has a direct effect on how your app scales because at lower concurrency levels, you need more instances to handle the event-driven demand for a function. While you can control and fine tune the concurrency, we provide defaults that work for most cases.

To learn how to set concurrency limits for HTTP trigger functions, see [Set HTTP concurrency limits](flex-consumption-how-to#set-http-concurrency-limits). To learn how to set concurrency limits for non-HTTP trigger functions, see [Target Base Scaling](functions-target-based-scaling).

## Deployment

Deployments in the Flex Consumption plan follow a single path, and there's no longer the need for app settings to influence deployment behavior. Your project code is built and zipped into an application package, then deployed to a blob storage container. On startup, your app gets the package and runs your function code from this package. By default, the same storage account used to store internal host metadata (AzureWebJobsStorage) is also used as the deployment container. However, you can use an alternative storage account or choose your preferred authentication method by [configuring your app's deployment settings](flex-consumption-how-to#configure-deployment-settings).

Tip

A **Flex Function App deployment details** diagnostic tool is available in the Azure portal. Open your Flex Consumption app, select **Diagnose and solve problems**, and search for `Flex Function App deployment details`

. This tool displays detailed information about your deployments, including deployment history, package status, and troubleshooting recommendations.

### Zero-downtime deployments

Note

Zero-downtime deployments with rolling updates are currently in public preview.

Flex Consumption provides zero-downtime deployments through rolling updates as the [site update strategy](flex-consumption-site-updates), which allows code deployments and configuration changes to be applied gradually across instances without interrupting function execution. Other hosting plans use deployment slots to minimize downtime during deployments. For deployment options across all hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments).

## Billing

There are two modes by which your costs are determined when running your apps in the Flex Consumption plan. Each mode is determined on a per-instance basis.

| Billing mode | Description |
|---|---|
On Demand |
When running in on demand mode, you are billed only for the amount of time your function code is executing on your available instances. In on demand mode, no minimum instance count is required. You're billed for:• The total amount of memory provisioned while each on demand instance is actively executing functions (in GB-seconds), minus a free grant of GB-s per month.• The total number of executions, minus a free grant (number) of executions per month. |
Always ready |
You can configure one or more instances, assigned to specific trigger types (HTTP/Durable/Blob) and individual functions, that are always available to handle requests. When you have any always ready instances enabled, you're billed for: • The total amount of memory provisioned across all of your always ready instances, known as the baseline (in GB-seconds).• The total amount of memory provisioned during the time each always ready instance is actively executing functions (in GB-seconds).• The total number of executions. In always ready billing, there are no free grants. |

For the most up-to-date information on execution pricing, always ready baseline costs, and free grants for on demand executions, see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/#pricing).

The minimum billable execution period for both execution modes is 1,000 ms. Past that, the billable activity period is rounded up to the nearest 100 ms. You can find details on the Flex Consumption plan billing meters in the [Monitoring reference](monitor-functions-reference?tab=flex-consumption-plan#metrics).

For details about how costs are calculated when you run in a Flex Consumption plan, including examples, see [Consumption-based costs](functions-consumption-costs?tabs=flex-consumption-plan#consumption-based-costs) and [Viewing cost-related data](functions-consumption-costs?tabs=flex-consumption-plan#viewing-and-estimating-costs-from-metrics).

## Supported language stack versions

This table shows the language stack versions that are currently supported for Flex Consumption apps:

| Language stack | Required version |
|---|---|
C# (isolated worker model)1 |
.NET 8, .NET 9, .NET 10 |
| Java | Java 11, Java 17, Java 21 |
| Node.js | Node.js 20, Node.js 22 |
| PowerShell | PowerShell 7.4 |
| Python | Python 3.10, Python 3.11, Python 3.12 |

- The
[C# in-process model](functions-dotnet-class-library)isn't supported. You instead need to[migrate your .NET project to the isolated worker model](migrate-dotnet-to-isolated-model).

## Regional subscription memory quotas

All Flex Consumption apps in a subscription and region share a compute quota, like a shared bucket of resources. This quota applies only to Flex Consumption apps — other hosting plans like Consumption, Premium, and Dedicated don't count against it. The quota limits how much total compute your Flex Consumption apps can use at the same time. If your apps try to exceed the quota, some executions and deployments might be delayed or fail, and scaling is throttled. However, you can still create new apps.

### Default quota

Each region in a subscription has a default quota of **250 cores** (equivalent to **512,000 MB**) for all Flex Consumption app instances combined. You can use any combination of instance sizes and counts, as long as the total cores stay under the quota.

To calculate the cores used, multiply the cores per instance by the number of instances:

| Instance size | Cores per instance | Formula |
|---|---|---|
| 512 MB | 0.25 | instances × 0.25 |
| 2,048 MB | 1 | instances × 1 |
| 4,096 MB | 2 | instances × 2 |

### Quota examples

Each of these scenarios reaches the 250 core quota limit. When the quota is reached, apps in the region stop scaling:

| Scenario | Calculation | Total cores |
|---|---|---|
| One 512-MB app at 1,000 instances | 1,000 × 0.25 | 250 |
| Two 512-MB apps at 250 and 750 instances | (250 + 750) × 0.25 | 250 |
| One 2,048-MB app at 250 instances | 250 × 1 | 250 |
| Two 2,048-MB apps at 100 and 150 instances | (100 + 150) × 1 | 250 |
| One 4,096-MB app at 125 instances | 125 × 2 | 250 |
| One 4,096-MB app at 100 instances + one 2,048-MB app at 50 instances | (100 × 2) + (50 × 1) | 250 |

### Important notes

- Flex Consumption scales rapidly based on
[concurrency](#concurrency)settings, so apps frequently acquire and release cores from the quota as demand changes. - Flex Consumption apps that scale to zero, or instances marked to be scaled in and deleted, don't count against the quota.
- Always ready instances count against quota.
- A
**Flex Consumption Quota tool**is available in the Azure portal. Open any Flex Consumption app in your subscription, select**Diagnose and solve problems**, search for`Flex Consumption Quota`

, then choose a region. The tool displays recommendations, current quota information, and historical usage views. - This quota can be increased pending capacity review. For example, from 250 cores to 1,000 cores or more. To request a larger quota, create a support ticket or contact your Microsoft account team.

## Deprecated properties and settings

In the Flex Consumption plan, many standard application settings and site configuration properties are deprecated or moved. Don't use these settings when you automate function app resource creation. For more information, see [Flex Consumption plan deprecations](functions-app-settings#flex-consumption-plan-deprecations).

## Considerations

Keep these other considerations in mind when using Flex Consumption plan:

**Apps per Plan**: Only one app is allowed per Flex Consumption plan.**Host**: There's a 30-second time-out for app initialization. When your function app takes longer than 30 seconds to start, you might see gRPC-related`System.TimeoutException`

entries logged. You can't currently configure this time-out. For more information, see[this host work item](https://github.com/Azure/azure-functions-host/issues/10482).**Durable Functions**: Azure Storage and Durable Task Scheduler are the only supported[storage providers](durable/durable-functions-storage-providers)for Durable Functions when hosted in the Flex Consumption plan. See[recommendations](durable/durable-functions-azure-storage-provider#flex-consumption-plan)when hosting Durable Functions in the Flex Consumption plan.**Virtual network integration and Resource provider registration**: You must have the`Microsoft.App`

Azure resource provider registered in your subscription to integrate to a virtual network, which is needed for subnet delegation. The Azure portal and Azure CLI enforce registration at app creation time since virtual network integration can be enabled at any point after your app is created. To register this provider,[follow these instructions](/en-us/azure/azure-resource-manager/management/resource-providers-and-types#register-resource-provider). The subnet delegation required by Flex Consumption apps is`Microsoft.App/environments`

.**Triggers**: While all triggers are fully supported in a Flex Consumption plan, the Blob storage trigger only supports the[Event Grid source](functions-event-grid-blob-trigger). Non-C# function apps must use version`[4.0.0, 5.0.0)`

of the[extension bundle](extension-bundles), or a later version.**Regions**: While the Flex Consumption plan is available in many Azure regions, not all regions are currently supported. To learn more, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Deployments**: Deployment slots aren't currently supported. For zero downtime deployments with Flex Consumption, see[Site update strategies in Flex Consumption](flex-consumption-site-updates).**Azure Storage as a local share**: Network File System (NFS) file shares aren't available for Flex Consumption. Only Server Message Block (SMB) and Azure Blobs (read-only) are supported.**Scale**: The lowest maximum scale is currently`40`

. The highest currently supported value is`1000`

.**PowerShell Managed dependencies**: Flex Consumption doesn't support[managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature). You must instead[upload modules with app content](functions-reference-powershell#including-modules-in-app-content).**Certificates**: Loading certificates with the WEBSITE_LOAD_CERTIFICATES app setting, managed certificates, app service certificates, and other platform certificate-based features like endToEndEncryptionEnabled are currently not supported.**Timezones**:`WEBSITE_TIME_ZONE`

and`TZ`

app settings aren't currently supported when running on Flex Consumption plan.**Azure Functions Runtime Version and Proxies**: Flex Consumption only supports version 4.x and later of the Azure Functions runtime. Azure Functions proxies was a feature of versions 1.x through 3.x of the Azure Functions runtime and is not available in Flex Consumption.

## Related articles

[Azure Functions hosting options](functions-scale)
[Create and manage function apps in the Flex Consumption plan](flex-consumption-how-to)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-mobile-apps -->

# Mobile Apps bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

Azure Mobile Apps bindings are only available to Azure Functions 1.x. They are not supported in Azure Functions 2.x and higher.

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

This article explains how to work with [Azure Mobile Apps](/en-us/previous-versions/azure/app-service-mobile/app-service-mobile-value-prop) bindings in Azure Functions. Azure Functions supports input and output bindings for Mobile Apps.

The Mobile Apps bindings let you read and update data tables in mobile apps.

## Packages - Functions 1.x

Mobile Apps bindings are provided in the [Microsoft.Azure.WebJobs.Extensions.MobileApps](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.MobileApps) NuGet package, version 1.x. Source code for the package is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.MobileApps/) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Input

The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function. In C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.

## Input - example

See the language-specific example:

The following example shows a Mobile Apps input binding in a *function.json* file and a [C# script function](functions-reference-csharp) that uses the binding. The function is triggered by a queue message that has a record identifier. The function reads the specified record and modifies its `Text`

property.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"queueName": "myqueue-items",
"connection": "",
"type": "queueTrigger",
"direction": "in"
},
{
"name": "record",
"type": "mobileTable",
"tableName": "MyTable",
"id": "{queueTrigger}",
"connection": "My_MobileApp_Url",
"apiKey": "My_MobileApp_Key",
"direction": "in"
}
]
}
```


The [configuration](#input---configuration) section explains these properties.

Here's the C# script code:

```
#r "Newtonsoft.Json"
using Newtonsoft.Json.Linq;
public static void Run(string myQueueItem, JObject record)
{
if (record != null)
{
record["Text"] = "This has changed.";
}
}
```


## Input - attributes

In [C# class libraries](functions-dotnet-class-library), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [the following configuration section](#input---configuration).

## Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to "mobileTable" |
direction |
n/a | Must be set to "in" |
name |
n/a | Name of input parameter in function signature. |
tableName |
TableName |
Name of the mobile app's data table |
id |
Id |
The identifier of the record to retrieve. Can be static or based on the trigger that invokes the function. For example, if you use a queue trigger for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve. |
connection |
Connection |
The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `https://<appname>.azurewebsites.net` . |
apiKey |
ApiKey |
The name of an app setting that has your mobile app's API key. Provide the API key if you implement an API key in your Node.js mobile app, or implement an API key in your .NET mobile app. To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## Input - usage

In C# functions, when the record with the specified ID is found, it is passed into the named
[JObject](https://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter. When the record is not found, the parameter value is `null`

.

In JavaScript functions, the record is passed into the `context.bindings.<name>`

object. When the record is not found, the parameter value is `null`

.

In C# and F# functions, any changes you make to the input record (input parameter) are automatically sent back to the table when the function exits successfully. You can't modify a record in JavaScript functions.

## Output

Use the Mobile Apps output binding to write a new record to a Mobile Apps table.

## Output - example

The following example shows a [C# function](functions-dotnet-class-library) that is triggered by a queue message and creates a record in a mobile app table.

```
[FunctionName("MobileAppsOutput")]
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
TraceWriter log)
{
return new { Text = $"I'm running in a C# function! {myQueueItem}" };
}
```


## Output - attributes

In [C# class libraries](functions-dotnet-class-library), use the [MobileTable](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.MobileApps/MobileTableAttribute.cs) attribute.

For information about attribute properties that you can configure, see [Output - configuration](#output---configuration). Here's a `MobileTable`

attribute example in a method signature:

```
[FunctionName("MobileAppsOutput")]
[return: MobileTable(ApiKeySetting = "MyMobileAppKey", TableName = "MyTable", MobileAppUriSetting = "MyMobileAppUri")]
public static object Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
TraceWriter log)
{
...
}
```


## Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `MobileTable`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to "mobileTable" |
direction |
n/a | Must be set to "out" |
name |
n/a | Name of output parameter in function signature. |
tableName |
TableName |
Name of the mobile app's data table |
connection |
MobileAppUriSetting |
The name of an app setting that has the mobile app's URL. The function uses this URL to construct the required REST operations against your mobile app. Create an app setting in your function app that contains the mobile app's URL, then specify the name of the app setting in the `connection` property in your input binding. The URL looks like `https://<appname>.azurewebsites.net` . |
apiKey |
ApiKeySetting |
The name of an app setting that has your mobile app's API key. Provide the API key if you implement an API key in your Node.js mobile app backend, or implement an API key in your .NET mobile app backend. To provide the key, create an app setting in your function app that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Important

Don't share the API key with your mobile app clients. It should only be distributed securely to service-side clients, like Azure Functions. Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository. This safeguards your sensitive information.

## Output - usage

In C# script functions, use a named output parameter of type `out object`

to access the output record. In C# class libraries, the `MobileTable`

attribute can be used with any of the following types:

`ICollector<T>`

or`IAsyncCollector<T>`

, where`T`

is either`JObject`

or any type with a`public string Id`

property.`out JObject`

`out T`

or`out T[]`

, where`T`

is any Type with a`public string Id`

property.

In Node.js functions, use `context.bindings.<name>`

to access the output record.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reliable-event-processing -->

# Reliable event processing with Azure Functions and Event Hubs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to build robust, reliable serverless solutions using Azure Functions with Azure Event Hubs triggers. This article covers best practices for checkpoints, error handling, and implementing circuit breaker patterns to ensure no events are lost and your event-driven applications remain stable and resilient.

## Challenges of event streams in distributed systems

Consider a system that sends events at a constant rate of 100 events per second. At this rate, within minutes multiple parallel instances can consume the incoming 100 events every second.

However, consider these challenges to consuming an event stream:

- An event publisher sends a corrupt event.
- Your function code encounters an unhandled exception.
- A downstream system goes offline and blocks event processing.

Unlike an Azure Queue storage trigger, which locks messages during processing, Azure Event Hubs reads, per partition, from a single point in the stream. This read behavior, which is more like a video player, provides the desired benefits of high-throughput, multiple consumer groups, and replay-ability. Events are read, forward or backward, from a checkpoint, but you must move the pointer to process new events. For more information, see [Checkpoint](../event-hubs/event-processor-balance-partition-load#checkpoint) in the Event Hubs documentation.

When errors occur in a stream and you choose not to advance the pointer, further event processing is blocked. In other words, should you stop the pointer to deal with an issue processing a single event, the unprocessed events begin piling up.

Functions avoids deadlocks by always advancing the stream's pointer, regardless of success or failure. Because the pointer keeps advancing, your functions need to deal with failures appropriately.

## How the Event Hubs trigger consumes events

Azure Functions consumes events from an event hub by cycling through the following steps:

- A pointer is created and persisted in Azure Storage for each partition of the event hub.
- New events are received in a batch (by default), and the host tries to trigger the function supplying a the batch of events for processing.
- When the function completes execution, with or without exceptions, the pointer is advanced and a checkpoint is saved to the default host storage account.
- Should conditions prevent function execution from completing, the host can't advance the pointer. When the pointer can't advance, subsequent executions reprocess the same events.

This behavior reveals a few important points:

Unhandled exceptions might cause you to lose events:

Function executions that raise an exception continue to progress the pointer. Setting a

[retry policy](#retry-policies)or other retry logic delays advancing the pointer until the entire retry completes.Functions guarantees

*at-least-once*delivery:Your code and dependent systems might need to account for the fact that the same event could be processed twice. For more information, see

[Designing Azure Functions for identical input](functions-idempotent).

## Handling exceptions

While all function code should include a [try/catch block](functions-bindings-error-pages) at the highest level of code, having a `catch`

block is even more important for functions that consume Event Hubs events. That way, when an exception is raised, the catch block handles the error before the pointer progresses.

## Retry mechanisms and policies

Because many exceptions in the cloud are transient, the first step in error handling is always to retry the operation. You can apply built-in retry policies or define your own retry logic.

### Retry policies

Functions provides built-in retry policies for Event Hubs. When using retry policies, you simply raise a new exception and the host try to process the event again based on the defined policy. This retry behavior requires version 5.x or later of the Event Hubs extension. For more information, see [Retry policies](functions-bindings-error-pages#retry-policies).

### Custom retry logic

You can also define your own retry logic in the function itself. For example, you could implement a policy that follows a workflow illustrated by the following rules:

- Try to process an event three times (potentially with a delay between retries).
- If the eventual outcome of all retries is a failure, then add an event to a queue so processing can continue on the stream.
- Corrupt or unprocessed events are then handled later.

Note

[Polly](https://github.com/App-vNext/Polly) is an example of a resilience and transient-fault-handling library for C# applications.

## Nonexception errors

Some issues can occur without an exception being raised. For example, consider a case where a request times out or the instance running the function crashes. When a function fails to complete without an exception, the offset pointer is never advanced. If the pointer doesn't advance, then any instance that runs after a failed execution continues to read the same events. This situation provides an *at-least-once* guarantee.

The assurance that every event is processed at least one time implies that some events could be processed more than once. Your function apps need to be aware of this possibility and must be built around the [principles of idempotency](functions-idempotent).

## Handling failure states

Your app might be able to acceptably handle a few errors in event processing. However, you should also be prepared to handle persistent failure state, which might occur as a result of failures in downstream processing. In such a failure state, such as a downstream data store being offline, your function should stop triggering on events until the system reaches a healthy state.

### Circuit breaker pattern

When you implement the *circuit breaker* pattern, your app can effectively pause event processing and then resume it at a later time after issues are resolved.

There are two components required to implement a circuit breaker in an event stream process:

- Shared state across all instances to track and monitor health of the circuit.
- A primary process that can manage the circuit state, as either
`open`

or`closed`

.

Implementation details can vary, but to share state among instances you need a storage mechanism. You can store state in Azure Storage, a Redis cache, or any other persistent service that can be accessed by your function app instances.

Both [Durable Functions](durable/durable-functions-overview) and [Azure Logic Apps](../logic-apps/logic-apps-overview) provide infrastructure to manage workflows and circuit states. This article describes using Logic Apps to pause and restart function executions, giving you the control required to implement the circuit breaker pattern.

### Define a failure threshold across instances

Persisted shared external state is required to monitor the health of the circuit when multiple instances are processing events simultaneously. You can then monitor this persisted state based on rules that indicate a failure state, such as:

When there are more than 100 event failures within a 30-second period across all instances, break the circuit to stop triggering on new events.


The implementation details for this monitoring logic vary depending on your specific app needs, but in general you must create a system that:

- Logs failures to persisted storage.
- Inspect the rolling count when new failures are logged to determine if the event failure threshold is met.
- When this threshold is met, emit an event telling the system to break the circuit.

### Managing circuit state with Azure Logic Apps

Azure Logic Apps comes with built-in connectors to different services, features, and stateful orchestrations, and it's a natural choice to manage circuit state. After detecting when a circuit must break, you can build a logic app to implement this workflow:

- Trigger an Event Grid workflow that stops the function processing.
- Send a notification email that includes an option to restart the workflow.

To learn how to disable and reenable specific functions using app settings, see [How to disable functions in Azure Functions](disable-function).

The email recipient can investigate the health of the circuit and, when appropriate, restart the circuit via a link in the notification email. As the workflow restarts the function, events are processed from the last event hub checkpoint.

When you use this approach, no events are lost, events are processed in order, and you can break the circuit as long as necessary.

## Migration strategies for Event Grid triggers

When you migrate an existing function app between regions or between some plans, you must recreate the app during the migration process. In this case, during the migration process, you might have two apps that are both able to consume from the same event stream and write to the same output destination.

You should consider [using consumer groups](../event-hubs/event-hubs-features#consumer-groups) to avoid event data loss or duplication during the migration process:

Create a new consumer group for the new target app.

Configure the trigger in the new app to use this new consumer group.

This allows both apps to process events independently during validation.

Validate that the new app is processing events correctly.

Stop the original app or remove its subscription/consumer group.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2 -->

# Azure Cosmos DB trigger and bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Cosmos DB](/en-us/azure/cosmos-db/serverless-computing-database) bindings in Azure Functions. Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB. For an end-to-end scenario that uses the Azure Cosmos DB extension, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

| Action | Type |
|---|---|
| Run a function when an Azure Cosmos DB document is created or modified |
|

[Input binding](functions-bindings-cosmosdb-v2-input)[Output binding](functions-bindings-cosmosdb-v2-output)Important

This version of the Azure Cosmos DB binding extension supports [Azure Functions version 4.x](functions-versions). If your app still uses version 1.x of the Functions runtime, instead see [Azure Cosmos DB bindings for Azure Functions 1.x](functions-bindings-cosmosdb).
In the Functions v1.x runtime, this binding was originally named `DocumentDB`

.

## Supported APIs

This table indicates how to connect to the various Azure Cosmos DB APIs from your function code:

## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The process for installing the extension varies depending on the extension version:

This version of the Azure Cosmos DB bindings extension introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.CosmosDB/), version 4.x.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureCosmosDBExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureCosmosDBExtension() |> ignore
) |> ignore
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

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos)is in preview.

**Cosmos DB trigger**

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

**Cosmos DB input binding**

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

**Cosmos DB output binding**

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Type support for Azure Cosmos is in Preview. Follow the [Python SDK Bindings for CosmosDB Sample](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python) to get started with SDK Types for Cosmos in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| CosmosDB input |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_containerproxy/function_app.py)`ContainerProxy`

[,](https://github.com/Azure/azure-functions-python-extensions/tree/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_cosmosclient/function_app.py)`CosmosClient`

`DatabaseProxy`

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

```
{
"version": "2.0",
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway",
"userAgentSuffix": "MyDesiredUserAgentStamp"
}
}
}
```


| Property | Default | Description |
|---|---|---|
connectionMode |
`Gateway` |
The connection mode used by the function when connecting to the Azure Cosmos DB service. Options: `Direct` connects directly to backend replicas over TCP and can provide lower latency, and `Gateway` routes requests through a front-end gateway over HTTPS. For more information, see
|
userAgentSuffix |
n/a | Adds the specified string value to all requests made by the trigger or binding to the service. This makes it easier for you to track the activity in Azure Monitor, based on a specific function app and filtering by `User Agent` . |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistant-trigger -->

# Azure OpenAI assistant trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant trigger lets you run your code based on custom chat bot or skill request made to an assistant.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
[Function(nameof(AddTodo))]
public Task AddTodo([AssistantSkillTrigger("Create a new todo task")] string taskDescription)
{
if (string.IsNullOrEmpty(taskDescription))
{
throw new ArgumentException("Task description cannot be empty");
}
this.logger.LogInformation("Adding todo: {task}", taskDescription);
string todoId = Guid.NewGuid().ToString()[..6];
return this.todoManager.AddTodoAsync(new TodoItem(todoId, taskDescription));
}
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
/**
* Called by the assistant to create new todo tasks.
*/
@FunctionName("AddTodo")
public void addTodo(
@AssistantSkillTrigger(
name = "assistantSkillCreateTodo",
functionDescription = "Create a new todo task"
) String taskDescription,
final ExecutionContext context) {
if (taskDescription == null || taskDescription.isEmpty()) {
throw new IllegalArgumentException("Task description cannot be empty");
}
context.getLogger().info("Adding todo: " + taskDescription);
String todoId = UUID.randomUUID().toString().substring(0, 6);
TodoItem todoItem = new TodoItem(todoId, taskDescription);
todoManager.addTodo(todoItem);
}
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
const { app, trigger } = require("@azure/functions");
const { TodoItem, CreateTodoManager } = require("../services/todoManager");
const { randomUUID } = require('crypto');
const todoManager = CreateTodoManager()
app.generic('AddTodo', {
trigger: trigger.generic({
type: 'assistantSkillTrigger',
functionDescription: 'Create a new todo task'
}),
handler: async (taskDescription, context) => {
if (!taskDescription) {
throw new Error('Task description cannot be empty')
}
context.log(`Adding todo: ${taskDescription}`)
const todoId = randomUUID().substring(0, 6)
return todoManager.AddTodo(new TodoItem(todoId, taskDescription))
}
})
```


```
import { InvocationContext, app, trigger } from "@azure/functions"
import { TodoItem, ITodoManager, CreateTodoManager } from "../services/todoManager"
import { randomUUID } from 'crypto';
const todoManager: ITodoManager = CreateTodoManager()
app.generic('AddTodo', {
trigger: trigger.generic({
type: 'assistantSkillTrigger',
functionDescription: 'Create a new todo task'
}),
handler: async (taskDescription: string, context: InvocationContext) => {
if (!taskDescription) {
throw new Error('Task description cannot be empty')
}
context.log(`Adding todo: ${taskDescription}`)
const todoId = randomUUID().substring(0, 6)
return todoManager.AddTodo(new TodoItem(todoId, taskDescription))
}
})
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

Here's the *function.json* file for Add Todo:

```
{
"bindings": [
{
"name": "TaskDescription",
"type": "assistantSkillTrigger",
"dataType": "string",
"direction": "in",
"functionDescription": "Create a new todo task"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($TaskDescription, $TriggerMetadata)
$ErrorActionPreference = "Stop"
if (-not $TaskDescription) {
throw "Task description cannot be empty"
}
Write-Information "Adding todo: $TaskDescription"
$todoID = [Guid]::NewGuid().ToString().Substring(0, 5)
Add-Todo $todoId $TaskDescription
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
@skills.function_name("AddTodo")
@skills.assistant_skill_trigger(
arg_name="taskDescription", function_description="Create a new todo task"
)
def add_todo(taskDescription: str) -> None:
if not taskDescription:
raise ValueError("Task description cannot be empty")
logging.info(f"Adding todo: {taskDescription}")
todo_id = str(uuid.uuid4())[0:6]
todo_manager.add_todo(TodoItem(id=todo_id, task=taskDescription))
return
```


## Attributes

Apply the `AssistantSkillTrigger`

attribute to define an assistant trigger, which supports these parameters:

| Parameter | Description |
|---|---|
FunctionDescription |
Gets the description of the assistant function, which is provided to the model. |
FunctionName |
Optional. Gets or sets the name of the function called by the assistant. |
ParameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Annotations

The `AssistantSkillTrigger`

annotation enables you to define an assistant trigger, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
functionDescription |
Gets the description of the assistant function, which is provided to the model. |
functionName |
Optional. Gets or sets the name of the function called by the assistant. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Decorators

During the preview, define the input binding as a `generic_trigger`

binding of type `assistantSkillTrigger`

, which supports these parameters:

| Parameter | Description |
|---|---|
function_description |
Gets the description of the assistant function, which is provided to the model. |
function_name |
Optional. Gets or sets the name of a function called by the assistant. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `AssistantSkillTrigger` . |
direction |
Must be `in` . |
name |
The name of the trigger. |
functionName |
Gets or sets the name of the function called by the assistant. |
functionDescription |
Gets the description of the assistant function, which is provided to the language model. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
type |
Must be `AssistantSkillTrigger` . |
name |
The name of the trigger. |
functionName |
Gets or sets the name of the function called by the assistant. |
functionDescription |
Gets the description of the assistant function, which is provided to the LLM |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

See the [Example section](#example) for complete examples.

## Usage

When `parameterDescriptionJson`

JSON value isn't provided, it's autogenerated. For more information on the syntax of this object, see the [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat/create#chat-create-tools).
