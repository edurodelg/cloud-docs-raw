---
source_url: https://google.github.io/adk-docs/artifacts/
fetched_at: 2026-01-30T23:34:42.279708
---

# Artifacts¶

# Artifacts[¶](#artifacts)

In ADK, **Artifacts** represent a crucial mechanism for managing named, versioned binary data associated either with a specific user interaction session or persistently with a user across multiple sessions. They allow your agents and tools to handle data beyond simple text strings, enabling richer interactions involving files, images, audio, and other binary formats.

Note

The specific parameters or method names for the primitives may vary slightly by SDK language (e.g., `save_artifact`

in Python, `saveArtifact`

in Java). Refer to the language-specific API documentation for details.

## What are Artifacts?[¶](#what-are-artifacts)

-
**Definition:**An Artifact is essentially a piece of binary data (like the content of a file) identified by a unique`filename`

string within a specific scope (session or user). Each time you save an artifact with the same filename, a new version is created. -
**Representation:**Artifacts are consistently represented using the standard`google.genai.types.Part`

object. The core data is typically stored within an inline data structure of the`Part`

(accessed via`inline_data`

), which itself contains:`data`

: The raw binary content as bytes.`mime_type`

: A string indicating the type of the data (e.g.,`"image/png"`

,`"application/pdf"`

). This is essential for correctly interpreting the data later.


# Example of how an artifact might be represented as a types.Part
import google.genai.types as types
# Assume 'image_bytes' contains the binary data of a PNG image
image_bytes = b'\x89PNG\r\n\x1a\n...' # Placeholder for actual image bytes
image_artifact = types.Part(
inline_data=types.Blob(
mime_type="image/png",
data=image_bytes
)
)
# You can also use the convenience constructor:
# image_artifact_alt = types.Part.from_bytes(data=image_bytes, mime_type="image/png")
print(f"Artifact MIME Type: {image_artifact.inline_data.mime_type}")
print(f"Artifact Data (first 10 bytes): {image_artifact.inline_data.data[:10]}...")


import type { Part } from '@google/genai';
import { createPartFromBase64 } from '@google/genai';
// Assume 'imageBytes' contains the binary data of a PNG image
const imageBytes = new Uint8Array([0x89, 0x50, 0x4e, 0x47, 0x0d, 0x0a, 0x1a, 0x0a]); // Placeholder
const imageArtifact: Part = createPartFromBase64(imageBytes.toString('base64'), "image/png");
console.log(`Artifact MIME Type: ${imageArtifact.inlineData?.mimeType}`);
// Note: Accessing raw bytes would require decoding from base64.


import (
"log"
"google.golang.org/genai"
)
// Create a byte slice with the image data.
imageBytes, err := os.ReadFile("image.png")
if err != nil {
log.Fatalf("Failed to read image file: %v", err)
}
// Create a new artifact with the image data.
imageArtifact := &genai.Part{
InlineData: &genai.Blob{
MIMEType: "image/png",
Data: imageBytes,
},
}
log.Printf("Artifact MIME Type: %s", imageArtifact.InlineData.MIMEType)
log.Printf("Artifact Data (first 8 bytes): %x...", imageArtifact.InlineData.Data[:8])


import com.google.genai.types.Part;
import java.nio.charset.StandardCharsets;
public class ArtifactExample {
public static void main(String[] args) {
// Assume 'imageBytes' contains the binary data of a PNG image
byte[] imageBytes = {(byte) 0x89, (byte) 0x50, (byte) 0x4E, (byte) 0x47, (byte) 0x0D, (byte) 0x0A, (byte) 0x1A, (byte) 0x0A, (byte) 0x01, (byte) 0x02}; // Placeholder for actual image bytes
// Create an image artifact using Part.fromBytes
Part imageArtifact = Part.fromBytes(imageBytes, "image/png");
System.out.println("Artifact MIME Type: " + imageArtifact.inlineData().get().mimeType().get());
System.out.println(
"Artifact Data (first 10 bytes): "
+ new String(imageArtifact.inlineData().get().data().get(), 0, 10, StandardCharsets.UTF_8)
+ "...");
}
}


**Persistence & Management:**Artifacts are not stored directly within the agent or session state. Their storage and retrieval are managed by a dedicated**Artifact Service**(an implementation of`BaseArtifactService`

, defined in`google.adk.artifacts`

. ADK provides various implementations, such as:- An in-memory service for testing or temporary storage (e.g.,
`InMemoryArtifactService`

in Python, defined in`google.adk.artifacts.in_memory_artifact_service.py`

). - A service for persistent storage using Google Cloud Storage (GCS) (e.g.,
`GcsArtifactService`

in Python, defined in`google.adk.artifacts.gcs_artifact_service.py`

). The chosen service implementation handles versioning automatically when you save data.

- An in-memory service for testing or temporary storage (e.g.,

## Why Use Artifacts?[¶](#why-use-artifacts)

While session `state`

is suitable for storing small pieces of configuration or conversational context (like strings, numbers, booleans, or small dictionaries/lists), Artifacts are designed for scenarios involving binary or large data:

**Handling Non-Textual Data:**Easily store and retrieve images, audio clips, video snippets, PDFs, spreadsheets, or any other file format relevant to your agent's function.**Persisting Large Data:**Session state is generally not optimized for storing large amounts of data. Artifacts provide a dedicated mechanism for persisting larger blobs without cluttering the session state.**User File Management:**Provide capabilities for users to upload files (which can be saved as artifacts) and retrieve or download files generated by the agent (loaded from artifacts).**Sharing Outputs:**Enable tools or agents to generate binary outputs (like a PDF report or a generated image) that can be saved via`save_artifact`

and later accessed by other parts of the application or even in subsequent sessions (if using user namespacing).**Caching Binary Data:**Store the results of computationally expensive operations that produce binary data (e.g., rendering a complex chart image) as artifacts to avoid regenerating them on subsequent requests.

In essence, whenever your agent needs to work with file-like binary data that needs to be persisted, versioned, or shared, Artifacts managed by an `ArtifactService`

are the appropriate mechanism within ADK.

## Common Use Cases[¶](#common-use-cases)

Artifacts provide a flexible way to handle binary data within your ADK applications.

Here are some typical scenarios where they prove valuable:

-
**Generated Reports/Files:**- A tool or agent generates a report (e.g., a PDF analysis, a CSV data export, an image chart).

-
**Handling User Uploads:**- A user uploads a file (e.g., an image for analysis, a document for summarization) through a front-end interface.

-
**Storing Intermediate Binary Results:**- An agent performs a complex multi-step process where one step generates intermediate binary data (e.g., audio synthesis, simulation results).

-
**Persistent User Data:**- Storing user-specific configuration or data that isn't a simple key-value state.

-
**Caching Generated Binary Content:**- An agent frequently generates the same binary output based on certain inputs (e.g., a company logo image, a standard audio greeting).


## Core Concepts[¶](#core-concepts)

Understanding artifacts involves grasping a few key components: the service that manages them, the data structure used to hold them, and how they are identified and versioned.

### Artifact Service (`BaseArtifactService`

)[¶](#artifact-service-baseartifactservice)

-
**Role:**The central component responsible for the actual storage and retrieval logic for artifacts. It defines*how*and*where*artifacts are persisted. -
**Interface:**Defined by the abstract base class`BaseArtifactService`

. Any concrete implementation must provide methods for:`Save Artifact`

: Stores the artifact data and returns its assigned version number.`Load Artifact`

: Retrieves a specific version (or the latest) of an artifact.`List Artifact keys`

: Lists the unique filenames of artifacts within a given scope.`Delete Artifact`

: Removes an artifact (and potentially all its versions, depending on implementation).`List versions`

: Lists all available version numbers for a specific artifact filename.

-
**Configuration:**You provide an instance of an artifact service (e.g.,`InMemoryArtifactService`

,`GcsArtifactService`

) when initializing the`Runner`

. The`Runner`

then makes this service available to agents and tools via the`InvocationContext`

.

from google.adk.runners import Runner
from google.adk.artifacts import InMemoryArtifactService # Or GcsArtifactService
from google.adk.agents import LlmAgent # Any agent
from google.adk.sessions import InMemorySessionService
# Example: Configuring the Runner with an Artifact Service
my_agent = LlmAgent(name="artifact_user_agent", model="gemini-2.0-flash")
artifact_service = InMemoryArtifactService() # Choose an implementation
session_service = InMemorySessionService()
runner = Runner(
agent=my_agent,
app_name="my_artifact_app",
session_service=session_service,
artifact_service=artifact_service # Provide the service instance here
)
# Now, contexts within runs managed by this runner can use artifact methods


import { InMemoryRunner } from '@google/adk';
import { LlmAgent } from '@google/adk';
import { InMemoryArtifactService } from '@google/adk';
// Example: Configuring the Runner with an Artifact Service
const myAgent = new LlmAgent({name: "artifact_user_agent", model: "gemini-2.5-flash"});
const artifactService = new InMemoryArtifactService(); // Choose an implementation
const sessionService = new InMemoryArtifactService();
const runner = new InMemoryRunner({
agent: myAgent,
appName: "my_artifact_app",
sessionService: sessionService,
artifactService: artifactService, // Provide the service instance here
});
// Now, contexts within runs managed by this runner can use artifact methods


import (
"context"
"log"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/artifactservice"
"google.golang.org/adk/llm/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/sessionservice"
"google.golang.org/genai"
)
// Create a new context.
ctx := context.Background()
// Set the app name.
const appName = "my_artifact_app"
// Create a new Gemini model.
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
log.Fatalf("Failed to create model: %v", err)
}
// Create a new LLM agent.
myAgent, err := llmagent.New(llmagent.Config{
Model: model,
Name: "artifact_user_agent",
Instruction: "You are an agent that describes images.",
BeforeModelCallbacks: []llmagent.BeforeModelCallback{
BeforeModelCallback,
},
})
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
// Create a new in-memory artifact service.
artifactService := artifact.InMemoryService()
// Create a new in-memory session service.
sessionService := session.InMemoryService()
// Create a new runner.
r, err := runner.New(runner.Config{
Agent: myAgent,
AppName: appName,
SessionService: sessionService,
ArtifactService: artifactService, // Provide the service instance here
})
if err != nil {
log.Fatalf("Failed to create runner: %v", err)
}
log.Printf("Runner created successfully: %v", r)


import com.google.adk.agents.LlmAgent;
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
import com.google.adk.artifacts.InMemoryArtifactService;
// Example: Configuring the Runner with an Artifact Service
LlmAgent myAgent = LlmAgent.builder()
.name("artifact_user_agent")
.model("gemini-2.0-flash")
.build();
InMemoryArtifactService artifactService = new InMemoryArtifactService(); // Choose an implementation
InMemorySessionService sessionService = new InMemorySessionService();
Runner runner = new Runner(myAgent, "my_artifact_app", artifactService, sessionService); // Provide the service instance here
// Now, contexts within runs managed by this runner can use artifact methods


### Artifact Data[¶](#artifact-data)

-
**Standard Representation:**Artifact content is universally represented using the`google.genai.types.Part`

object, the same structure used for parts of LLM messages. -
**Key Attribute (**For artifacts, the most relevant attribute is`inline_data`

):`inline_data`

, which is a`google.genai.types.Blob`

object containing:`data`

(`bytes`

): The raw binary content of the artifact.`mime_type`

(`str`

): A standard MIME type string (e.g.,`'application/pdf'`

,`'image/png'`

,`'audio/mpeg'`

) describing the nature of the binary data.**This is crucial for correct interpretation when loading the artifact.**


import google.genai.types as types
# Example: Creating an artifact Part from raw bytes
pdf_bytes = b'%PDF-1.4...' # Your raw PDF data
pdf_mime_type = "application/pdf"
# Using the constructor
pdf_artifact_py = types.Part(
inline_data=types.Blob(data=pdf_bytes, mime_type=pdf_mime_type)
)
# Using the convenience class method (equivalent)
pdf_artifact_alt_py = types.Part.from_bytes(data=pdf_bytes, mime_type=pdf_mime_type)
print(f"Created Python artifact with MIME type: {pdf_artifact_py.inline_data.mime_type}")


import type { Part } from '@google/genai';
import { createPartFromBase64 } from '@google/genai';
// Example: Creating an artifact Part from raw bytes
const pdfBytes = new Uint8Array([0x25, 0x50, 0x44, 0x46, 0x2d, 0x31, 0x2e, 0x34]); // Your raw PDF data
const pdfMimeType = "application/pdf";
const pdfArtifact: Part = createPartFromBase64(pdfBytes.toString('base64'), pdfMimeType);
console.log(`Created TypeScript artifact with MIME Type: ${pdfArtifact.inlineData?.mimeType}`);


import (
"log"
"os"
"google.golang.org/genai"
)
// Load imageBytes from a file
imageBytes, err := os.ReadFile("image.png")
if err != nil {
log.Fatalf("Failed to read image file: %v", err)
}
// genai.NewPartFromBytes is a convenience function that is a shorthand for
// creating a &genai.Part with the InlineData field populated.
// Create a new artifact from the image data.
imageArtifact := genai.NewPartFromBytes([]byte(imageBytes), "image/png")
log.Printf("Artifact MIME Type: %s", imageArtifact.InlineData.MIMEType)


import com.google.genai.types.Blob;
import com.google.genai.types.Part;
import java.nio.charset.StandardCharsets;
public class ArtifactDataExample {
public static void main(String[] args) {
// Example: Creating an artifact Part from raw bytes
byte[] pdfBytes = "%PDF-1.4...".getBytes(StandardCharsets.UTF_8); // Your raw PDF data
String pdfMimeType = "application/pdf";
// Using the Part.fromBlob() constructor with a Blob
Blob pdfBlob = Blob.builder()
.data(pdfBytes)
.mimeType(pdfMimeType)
.build();
Part pdfArtifactJava = Part.builder().inlineData(pdfBlob).build();
// Using the convenience static method Part.fromBytes() (equivalent)
Part pdfArtifactAltJava = Part.fromBytes(pdfBytes, pdfMimeType);
// Accessing mimeType, note the use of Optional
String mimeType = pdfArtifactJava.inlineData()
.flatMap(Blob::mimeType)
.orElse("unknown");
System.out.println("Created Java artifact with MIME type: " + mimeType);
// Accessing data
byte[] data = pdfArtifactJava.inlineData()
.flatMap(Blob::data)
.orElse(new byte[0]);
System.out.println("Java artifact data (first 10 bytes): "
+ new String(data, 0, Math.min(data.length, 10), StandardCharsets.UTF_8) + "...");
}
}


### Filename[¶](#filename)

**Identifier:**A simple string used to name and retrieve an artifact within its specific namespace.**Uniqueness:**Filenames must be unique within their scope (either the session or the user namespace).**Best Practice:**Use descriptive names, potentially including file extensions (e.g.,`"monthly_report.pdf"`

,`"user_avatar.jpg"`

), although the extension itself doesn't dictate behavior – the`mime_type`

does.

### Versioning[¶](#versioning)

**Automatic Versioning:**The artifact service automatically handles versioning. When you call`save_artifact`

, the service determines the next available version number (typically starting from 0 and incrementing) for that specific filename and scope.**Returned by**The`save_artifact`

:`save_artifact`

method returns the integer version number that was assigned to the newly saved artifact.**Retrieval:**`load_artifact(..., version=None)`

(default): Retrieves the*latest*available version of the artifact.`load_artifact(..., version=N)`

: Retrieves the specific version`N`

.**Listing Versions:**The`list_versions`

method (on the service, not context) can be used to find all existing version numbers for an artifact.

### Namespacing (Session vs. User)[¶](#namespacing-session-vs-user)

-
**Concept:**Artifacts can be scoped either to a specific session or more broadly to a user across all their sessions within the application. This scoping is determined by the`filename`

format and handled internally by the`ArtifactService`

. -
**Default (Session Scope):**If you use a plain filename like`"report.pdf"`

, the artifact is associated with the specific`app_name`

,`user_id`

,*and*`session_id`

. It's only accessible within that exact session context. -
**User Scope (**If you prefix the filename with`"user:"`

prefix):`"user:"`

, like`"user:profile.png"`

, the artifact is associated only with the`app_name`

and`user_id`

. It can be accessed or updated from*any*session belonging to that user within the app.

# Example illustrating namespace difference (conceptual)
# Session-specific artifact filename
session_report_filename = "summary.txt"
# User-specific artifact filename
user_config_filename = "user:settings.json"
# When saving 'summary.txt' via context.save_artifact,
# it's tied to the current app_name, user_id, and session_id.
# When saving 'user:settings.json' via context.save_artifact,
# the ArtifactService implementation should recognize the "user:" prefix
# and scope it to app_name and user_id, making it accessible across sessions for that user.


// Example illustrating namespace difference (conceptual)
// Session-specific artifact filename
const sessionReportFilename = "summary.txt";
// User-specific artifact filename
const userConfigFilename = "user:settings.json";
// When saving 'summary.txt' via context.saveArtifact, it's tied to the current appName, userId, and sessionId.
// When saving 'user:settings.json' via context.saveArtifact, the ArtifactService implementation recognizes the "user:" prefix and scopes it to appName and userId, making it accessible across sessions for that user.


import (
"log"
)
// Note: Namespacing is only supported when using the GCS ArtifactService implementation.
// A session-scoped artifact is only available within the current session.
sessionReportFilename := "summary.txt"
// A user-scoped artifact is available across all sessions for the current user.
userConfigFilename := "user:settings.json"
// When saving 'summary.txt' via ctx.Artifacts().Save,
// it's tied to the current app_name, user_id, and session_id.
// ctx.Artifacts().Save(sessionReportFilename, *artifact);
// When saving 'user:settings.json' via ctx.Artifacts().Save,
// the ArtifactService implementation should recognize the "user:" prefix
// and scope it to app_name and user_id, making it accessible across sessions for that user.
// ctx.Artifacts().Save(userConfigFilename, *artifact);


// Example illustrating namespace difference (conceptual)
// Session-specific artifact filename
String sessionReportFilename = "summary.txt";
// User-specific artifact filename
String userConfigFilename = "user:settings.json"; // The "user:" prefix is key
// When saving 'summary.txt' via context.save_artifact,
// it's tied to the current app_name, user_id, and session_id.
// artifactService.saveArtifact(appName, userId, sessionId1, sessionReportFilename, someData);
// When saving 'user:settings.json' via context.save_artifact,
// the ArtifactService implementation should recognize the "user:" prefix
// and scope it to app_name and user_id, making it accessible across sessions for that user.
// artifactService.saveArtifact(appName, userId, sessionId1, userConfigFilename, someData);


These core concepts work together to provide a flexible system for managing binary data within the ADK framework.

## Interacting with Artifacts (via Context Objects)[¶](#interacting-with-artifacts-via-context-objects)

The primary way you interact with artifacts within your agent's logic (specifically within callbacks or tools) is through methods provided by the `CallbackContext`

and `ToolContext`

objects. These methods abstract away the underlying storage details managed by the `ArtifactService`

.

### Prerequisite: Configuring the `ArtifactService`

[¶](#prerequisite-configuring-the-artifactservice)

Before you can use any artifact methods via the context objects, you **must** provide an instance of a [ BaseArtifactService implementation](#available-implementations) (like

[or](#inmemoryartifactservice)

`InMemoryArtifactService`

[) when initializing your](#gcsartifactservice)

`GcsArtifactService`

`Runner`

.In Python, you provide this instance when initializing your `Runner`

.

from google.adk.runners import Runner
from google.adk.artifacts import InMemoryArtifactService # Or GcsArtifactService
from google.adk.agents import LlmAgent
from google.adk.sessions import InMemorySessionService
# Your agent definition
agent = LlmAgent(name="my_agent", model="gemini-2.0-flash")
# Instantiate the desired artifact service
artifact_service = InMemoryArtifactService()
# Provide it to the Runner
runner = Runner(
agent=agent,
app_name="artifact_app",
session_service=InMemorySessionService(),
artifact_service=artifact_service # Service must be provided here
)


`artifact_service`

is configured in the `InvocationContext`

(which happens if it's not passed to the `Runner`

), calling `save_artifact`

, `load_artifact`

, or `list_artifacts`

on the context objects will raise a `ValueError`

.
import { LlmAgent, InMemoryRunner, InMemoryArtifactService } from '@google/adk';
// Your agent definition
const agent = new LlmAgent({name: "my_agent", model: "gemini-2.5-flash"});
// Instantiate the desired artifact service
const artifactService = new InMemoryArtifactService();
// Provide it to the Runner
const runner = new InMemoryRunner({
agent: agent,
appName: "artifact_app",
sessionService: new InMemoryArtifactService(),
artifactService: artifactService, // Service must be provided here
});
// If no artifactService is configured, calling artifact methods on context objects will throw an error.


`ArtifactService`

instance is not available (e.g., `null`

) when artifact operations are attempted, it would typically result in a `NullPointerException`

or a custom error, depending on how your application is structured. Robust applications often use dependency injection frameworks to manage service lifecycles and ensure availability.
import (
"context"
"log"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/artifactservice"
"google.golang.org/adk/llm/gemini"
"google.golang.org/adk/runner"
"google.golang.org/adk/sessionservice"
"google.golang.org/genai"
)
// Create a new context.
ctx := context.Background()
// Set the app name.
const appName = "my_artifact_app"
// Create a new Gemini model.
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{})
if err != nil {
log.Fatalf("Failed to create model: %v", err)
}
// Create a new LLM agent.
myAgent, err := llmagent.New(llmagent.Config{
Model: model,
Name: "artifact_user_agent",
Instruction: "You are an agent that describes images.",
BeforeModelCallbacks: []llmagent.BeforeModelCallback{
BeforeModelCallback,
},
})
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
// Create a new in-memory artifact service.
artifactService := artifact.InMemoryService()
// Create a new in-memory session service.
sessionService := session.InMemoryService()
// Create a new runner.
r, err := runner.New(runner.Config{
Agent: myAgent,
AppName: appName,
SessionService: sessionService,
ArtifactService: artifactService, // Provide the service instance here
})
if err != nil {
log.Fatalf("Failed to create runner: %v", err)
}
log.Printf("Runner created successfully: %v", r)


In Java, you would instantiate a `BaseArtifactService`

implementation and then ensure it's accessible to the parts of your application that manage artifacts. This is often done through dependency injection or by explicitly passing the service instance.

import com.google.adk.agents.LlmAgent;
import com.google.adk.artifacts.InMemoryArtifactService; // Or GcsArtifactService
import com.google.adk.runner.Runner;
import com.google.adk.sessions.InMemorySessionService;
public class SampleArtifactAgent {
public static void main(String[] args) {
// Your agent definition
LlmAgent agent = LlmAgent.builder()
.name("my_agent")
.model("gemini-2.0-flash")
.build();
// Instantiate the desired artifact service
InMemoryArtifactService artifactService = new InMemoryArtifactService();
// Provide it to the Runner
Runner runner = new Runner(agent,
"APP_NAME",
artifactService, // Service must be provided here
new InMemorySessionService());
}
}


### Accessing Methods[¶](#accessing-methods)

The artifact interaction methods are available directly on instances of `CallbackContext`

(passed to agent and model callbacks) and `ToolContext`

(passed to tool callbacks). Remember that `ToolContext`

inherits from `CallbackContext`

.

#### Saving Artifacts[¶](#saving-artifacts)

-
**Code Example:**[import google.genai.types as types](#__codelineno-20-1)[from google.adk.agents.callback_context import CallbackContext # Or ToolContext](#__codelineno-20-2)[async def save_generated_report_py(context: CallbackContext, report_bytes: bytes):](#__codelineno-20-4)["""Saves generated PDF report bytes as an artifact."""](#__codelineno-20-5)[report_artifact = types.Part.from_bytes(](#__codelineno-20-6)[data=report_bytes,](#__codelineno-20-7)[mime_type="application/pdf"](#__codelineno-20-8)[)](#__codelineno-20-9)[filename = "generated_report.pdf"](#__codelineno-20-10)[try:](#__codelineno-20-12)[version = await context.save_artifact(filename=filename, artifact=report_artifact)](#__codelineno-20-13)[print(f"Successfully saved Python artifact '{filename}' as version {version}.")](#__codelineno-20-14)[# The event generated after this callback will contain:](#__codelineno-20-15)[# event.actions.artifact_delta == {"generated_report.pdf": version}](#__codelineno-20-16)[except ValueError as e:](#__codelineno-20-17)[print(f"Error saving Python artifact: {e}. Is ArtifactService configured in Runner?")](#__codelineno-20-18)[except Exception as e:](#__codelineno-20-19)[# Handle potential storage errors (e.g., GCS permissions)](#__codelineno-20-20)[print(f"An unexpected error occurred during Python artifact save: {e}")](#__codelineno-20-21)[# --- Example Usage Concept (Python) ---](#__codelineno-20-23)[# async def main_py():](#__codelineno-20-24)[# callback_context: CallbackContext = ... # obtain context](#__codelineno-20-25)[# report_data = b'...' # Assume this holds the PDF bytes](#__codelineno-20-26)[# await save_generated_report_py(callback_context, report_data)](#__codelineno-20-27)[import type { Part } from '@google/genai';](#__codelineno-21-1)[import { createPartFromBase64 } from '@google/genai';](#__codelineno-21-2)[import { CallbackContext } from '@google/adk';](#__codelineno-21-3)[async function saveGeneratedReport(context: CallbackContext, reportBytes: Uint8Array): Promise<void> {](#__codelineno-21-5)[/**Saves generated PDF report bytes as an artifact.*/](#__codelineno-21-6)[const reportArtifact: Part = createPartFromBase64(reportBytes.toString('base64'), "application/pdf");](#__codelineno-21-7)[const filename = "generated_report.pdf";](#__codelineno-21-9)[try {](#__codelineno-21-11)[const version = await context.saveArtifact(filename, reportArtifact);](#__codelineno-21-12)[console.log(`Successfully saved TypeScript artifact '${filename}' as version ${version}.`);](#__codelineno-21-13)[} catch (e: any) {](#__codelineno-21-14)[console.error(`Error saving TypeScript artifact: ${e.message}. Is ArtifactService configured in Runner?`);](#__codelineno-21-15)[}](#__codelineno-21-16)[}](#__codelineno-21-17)[import (](#__codelineno-22-1)["log"](#__codelineno-22-2)["google.golang.org/adk/agent"](#__codelineno-22-4)["google.golang.org/adk/llm"](#__codelineno-22-5)["google.golang.org/genai"](#__codelineno-22-6)[)](#__codelineno-22-7)[// saveReportCallback is a BeforeModel callback that saves a report from session state.](#__codelineno-22-9)[func saveReportCallback(ctx agent.CallbackContext, req *model.LLMRequest) (*model.LLMResponse, error) {](#__codelineno-22-10)[// Get the report data from the session state.](#__codelineno-22-11)[reportData, err := ctx.State().Get("report_bytes")](#__codelineno-22-12)[if err != nil {](#__codelineno-22-13)[log.Printf("No report data found in session state: %v", err)](#__codelineno-22-14)[return nil, nil // No report to save, continue normally.](#__codelineno-22-15)[}](#__codelineno-22-16)[// Check if the report data is in the expected format.](#__codelineno-22-18)[reportBytes, ok := reportData.([]byte)](#__codelineno-22-19)[if !ok {](#__codelineno-22-20)[log.Printf("Report data in session state was not in the expected byte format.")](#__codelineno-22-21)[return nil, nil](#__codelineno-22-22)[}](#__codelineno-22-23)[// Create a new artifact with the report data.](#__codelineno-22-25)[reportArtifact := &genai.Part{](#__codelineno-22-26)[InlineData: &genai.Blob{](#__codelineno-22-27)[MIMEType: "application/pdf",](#__codelineno-22-28)[Data: reportBytes,](#__codelineno-22-29)[},](#__codelineno-22-30)[}](#__codelineno-22-31)[// Set the filename for the artifact.](#__codelineno-22-32)[filename := "generated_report.pdf"](#__codelineno-22-33)[// Save the artifact to the artifact service.](#__codelineno-22-34)[_, err = ctx.Artifacts().Save(ctx, filename, reportArtifact)](#__codelineno-22-35)[if err != nil {](#__codelineno-22-36)[log.Printf("An unexpected error occurred during Go artifact save: %v", err)](#__codelineno-22-37)[// Depending on requirements, you might want to return an error to the user.](#__codelineno-22-38)[return nil, nil](#__codelineno-22-39)[}](#__codelineno-22-40)[log.Printf("Successfully saved Go artifact '%s'.", filename)](#__codelineno-22-41)[// Return nil to continue to the next callback or the model.](#__codelineno-22-42)[return nil, nil](#__codelineno-22-43)[}](#__codelineno-22-44)[import com.google.adk.agents.CallbackContext;](#__codelineno-23-1)[import com.google.adk.artifacts.BaseArtifactService;](#__codelineno-23-2)[import com.google.adk.artifacts.InMemoryArtifactService;](#__codelineno-23-3)[import com.google.genai.types.Part;](#__codelineno-23-4)[import java.nio.charset.StandardCharsets;](#__codelineno-23-5)[public class SaveArtifactExample {](#__codelineno-23-7)[public void saveGeneratedReport(CallbackContext callbackContext, byte[] reportBytes) {](#__codelineno-23-9)[// Saves generated PDF report bytes as an artifact.](#__codelineno-23-10)[Part reportArtifact = Part.fromBytes(reportBytes, "application/pdf");](#__codelineno-23-11)[String filename = "generatedReport.pdf";](#__codelineno-23-12)[callbackContext.saveArtifact(filename, reportArtifact);](#__codelineno-23-14)[System.out.println("Successfully saved Java artifact '" + filename);](#__codelineno-23-15)[// The event generated after this callback will contain:](#__codelineno-23-16)[// event().actions().artifactDelta == {"generated_report.pdf": version}](#__codelineno-23-17)[}](#__codelineno-23-18)[// --- Example Usage Concept (Java) ---](#__codelineno-23-20)[public static void main(String[] args) {](#__codelineno-23-21)[BaseArtifactService service = new InMemoryArtifactService(); // Or GcsArtifactService](#__codelineno-23-22)[SaveArtifactExample myTool = new SaveArtifactExample();](#__codelineno-23-23)[byte[] reportData = "...".getBytes(StandardCharsets.UTF_8); // PDF bytes](#__codelineno-23-24)[CallbackContext callbackContext; // ... obtain callback context from your app](#__codelineno-23-25)[myTool.saveGeneratedReport(callbackContext, reportData);](#__codelineno-23-26)[// Due to async nature, in a real app, ensure program waits or handles completion.](#__codelineno-23-27)[}](#__codelineno-23-28)[}](#__codelineno-23-29)

#### Loading Artifacts[¶](#loading-artifacts)

-
**Code Example:**[import google.genai.types as types](#__codelineno-24-1)[from google.adk.agents.callback_context import CallbackContext # Or ToolContext](#__codelineno-24-2)[async def process_latest_report_py(context: CallbackContext):](#__codelineno-24-4)["""Loads the latest report artifact and processes its data."""](#__codelineno-24-5)[filename = "generated_report.pdf"](#__codelineno-24-6)[try:](#__codelineno-24-7)[# Load the latest version](#__codelineno-24-8)[report_artifact = await context.load_artifact(filename=filename)](#__codelineno-24-9)[if report_artifact and report_artifact.inline_data:](#__codelineno-24-11)[print(f"Successfully loaded latest Python artifact '{filename}'.")](#__codelineno-24-12)[print(f"MIME Type: {report_artifact.inline_data.mime_type}")](#__codelineno-24-13)[# Process the report_artifact.inline_data.data (bytes)](#__codelineno-24-14)[pdf_bytes = report_artifact.inline_data.data](#__codelineno-24-15)[print(f"Report size: {len(pdf_bytes)} bytes.")](#__codelineno-24-16)[# ... further processing ...](#__codelineno-24-17)[else:](#__codelineno-24-18)[print(f"Python artifact '{filename}' not found.")](#__codelineno-24-19)[# Example: Load a specific version (if version 0 exists)](#__codelineno-24-21)[# specific_version_artifact = await context.load_artifact(filename=filename, version=0)](#__codelineno-24-22)[# if specific_version_artifact:](#__codelineno-24-23)[# print(f"Loaded version 0 of '{filename}'.")](#__codelineno-24-24)[except ValueError as e:](#__codelineno-24-26)[print(f"Error loading Python artifact: {e}. Is ArtifactService configured?")](#__codelineno-24-27)[except Exception as e:](#__codelineno-24-28)[# Handle potential storage errors](#__codelineno-24-29)[print(f"An unexpected error occurred during Python artifact load: {e}")](#__codelineno-24-30)[# --- Example Usage Concept (Python) ---](#__codelineno-24-32)[# async def main_py():](#__codelineno-24-33)[# callback_context: CallbackContext = ... # obtain context](#__codelineno-24-34)[# await process_latest_report_py(callback_context)](#__codelineno-24-35)[import { CallbackContext } from '@google/adk';](#__codelineno-25-1)[async function processLatestReport(context: CallbackContext): Promise<void> {](#__codelineno-25-3)[/**Loads the latest report artifact and processes its data.*/](#__codelineno-25-4)[const filename = "generated_report.pdf";](#__codelineno-25-5)[try {](#__codelineno-25-6)[// Load the latest version](#__codelineno-25-7)[const reportArtifact = await context.loadArtifact(filename);](#__codelineno-25-8)[if (reportArtifact?.inlineData) {](#__codelineno-25-10)[console.log(`Successfully loaded latest TypeScript artifact '${filename}'.`);](#__codelineno-25-11)[console.log(`MIME Type: ${reportArtifact.inlineData.mimeType}`);](#__codelineno-25-12)[// Process the reportArtifact.inlineData.data (base64 string)](#__codelineno-25-13)[const pdfData = Buffer.from(reportArtifact.inlineData.data, 'base64');](#__codelineno-25-14)[console.log(`Report size: ${pdfData.length} bytes.`);](#__codelineno-25-15)[// ... further processing ...](#__codelineno-25-16)[} else {](#__codelineno-25-17)[console.log(`TypeScript artifact '${filename}' not found.`);](#__codelineno-25-18)[}](#__codelineno-25-19)[} catch (e: any) {](#__codelineno-25-21)[console.error(`Error loading TypeScript artifact: ${e.message}. Is ArtifactService configured?`);](#__codelineno-25-22)[}](#__codelineno-25-23)[}](#__codelineno-25-24)[import (](#__codelineno-26-1)["log"](#__codelineno-26-2)["google.golang.org/adk/agent"](#__codelineno-26-4)["google.golang.org/adk/llm"](#__codelineno-26-5)[)](#__codelineno-26-6)[// loadArtifactsCallback is a BeforeModel callback that loads a specific artifact](#__codelineno-26-8)[// and adds its content to the LLM request.](#__codelineno-26-9)[func loadArtifactsCallback(ctx agent.CallbackContext, req *model.LLMRequest) (*model.LLMResponse, error) {](#__codelineno-26-10)[log.Println("[Callback] loadArtifactsCallback triggered.")](#__codelineno-26-11)[// In a real app, you would parse the user's request to find a filename.](#__codelineno-26-12)[// For this example, we'll hardcode a filename to demonstrate.](#__codelineno-26-13)[const filenameToLoad = "generated_report.pdf"](#__codelineno-26-14)[// Load the artifact from the artifact service.](#__codelineno-26-16)[loadedPartResponse, err := ctx.Artifacts().Load(ctx, filenameToLoad)](#__codelineno-26-17)[if err != nil {](#__codelineno-26-18)[log.Printf("Callback could not load artifact '%s': %v", filenameToLoad, err)](#__codelineno-26-19)[return nil, nil // File not found or error, continue to model.](#__codelineno-26-20)[}](#__codelineno-26-21)[loadedPart := loadedPartResponse.Part](#__codelineno-26-23)[log.Printf("Callback successfully loaded artifact '%s'.", filenameToLoad)](#__codelineno-26-25)[// Ensure there's at least one content in the request to append to.](#__codelineno-26-27)[if len(req.Contents) == 0 {](#__codelineno-26-28)[req.Contents = []*genai.Content{{Parts: []*genai.Part{](#__codelineno-26-29)[genai.NewPartFromText("SYSTEM: The following file is provided for context:\n"),](#__codelineno-26-30)[}}}](#__codelineno-26-31)[}](#__codelineno-26-32)[// Add the loaded artifact to the request for the model.](#__codelineno-26-34)[lastContent := req.Contents[len(req.Contents)-1]](#__codelineno-26-35)[lastContent.Parts = append(lastContent.Parts, loadedPart)](#__codelineno-26-36)[log.Printf("Added artifact '%s' to LLM request.", filenameToLoad)](#__codelineno-26-37)[// Return nil to continue to the next callback or the model.](#__codelineno-26-39)[return nil, nil // Continue to next callback or LLM call](#__codelineno-26-40)[}](#__codelineno-26-41)[import com.google.adk.artifacts.BaseArtifactService;](#__codelineno-27-1)[import com.google.genai.types.Part;](#__codelineno-27-2)[import io.reactivex.rxjava3.core.MaybeObserver;](#__codelineno-27-3)[import io.reactivex.rxjava3.disposables.Disposable;](#__codelineno-27-4)[import java.util.Optional;](#__codelineno-27-5)[public class MyArtifactLoaderService {](#__codelineno-27-7)[private final BaseArtifactService artifactService;](#__codelineno-27-9)[private final String appName;](#__codelineno-27-10)[public MyArtifactLoaderService(BaseArtifactService artifactService, String appName) {](#__codelineno-27-12)[this.artifactService = artifactService;](#__codelineno-27-13)[this.appName = appName;](#__codelineno-27-14)[}](#__codelineno-27-15)[public void processLatestReportJava(String userId, String sessionId, String filename) {](#__codelineno-27-17)[// Load the latest version by passing Optional.empty() for the version](#__codelineno-27-18)[artifactService](#__codelineno-27-19)[.loadArtifact(appName, userId, sessionId, filename, Optional.empty())](#__codelineno-27-20)[.subscribe(](#__codelineno-27-21)[new MaybeObserver<Part>() {](#__codelineno-27-22)[@Override](#__codelineno-27-23)[public void onSubscribe(Disposable d) {](#__codelineno-27-24)[// Optional: handle subscription](#__codelineno-27-25)[}](#__codelineno-27-26)[@Override](#__codelineno-27-28)[public void onSuccess(Part reportArtifact) {](#__codelineno-27-29)[System.out.println(](#__codelineno-27-30)["Successfully loaded latest Java artifact '" + filename + "'.");](#__codelineno-27-31)[reportArtifact](#__codelineno-27-32)[.inlineData()](#__codelineno-27-33)[.ifPresent(](#__codelineno-27-34)[blob -> {](#__codelineno-27-35)[System.out.println(](#__codelineno-27-36)["MIME Type: " + blob.mimeType().orElse("N/A"));](#__codelineno-27-37)[byte[] pdfBytes = blob.data().orElse(new byte[0]);](#__codelineno-27-38)[System.out.println("Report size: " + pdfBytes.length + " bytes.");](#__codelineno-27-39)[// ... further processing of pdfBytes ...](#__codelineno-27-40)[});](#__codelineno-27-41)[}](#__codelineno-27-42)[@Override](#__codelineno-27-44)[public void onError(Throwable e) {](#__codelineno-27-45)[// Handle potential storage errors or other exceptions](#__codelineno-27-46)[System.err.println(](#__codelineno-27-47)["An error occurred during Java artifact load for '"](#__codelineno-27-48)[+ filename](#__codelineno-27-49)[+ "': "](#__codelineno-27-50)[+ e.getMessage());](#__codelineno-27-51)[}](#__codelineno-27-52)[@Override](#__codelineno-27-54)[public void onComplete() {](#__codelineno-27-55)[// Called if the artifact (latest version) is not found](#__codelineno-27-56)[System.out.println("Java artifact '" + filename + "' not found.");](#__codelineno-27-57)[}](#__codelineno-27-58)[});](#__codelineno-27-59)[// Example: Load a specific version (e.g., version 0)](#__codelineno-27-61)[/*](#__codelineno-27-62)[artifactService.loadArtifact(appName, userId, sessionId, filename, Optional.of(0))](#__codelineno-27-63)[.subscribe(part -> {](#__codelineno-27-64)[System.out.println("Loaded version 0 of Java artifact '" + filename + "'.");](#__codelineno-27-65)[}, throwable -> {](#__codelineno-27-66)[System.err.println("Error loading version 0 of '" + filename + "': " + throwable.getMessage());](#__codelineno-27-67)[}, () -> {](#__codelineno-27-68)[System.out.println("Version 0 of Java artifact '" + filename + "' not found.");](#__codelineno-27-69)[});](#__codelineno-27-70)[*/](#__codelineno-27-71)[}](#__codelineno-27-72)[// --- Example Usage Concept (Java) ---](#__codelineno-27-74)[public static void main(String[] args) {](#__codelineno-27-75)[// BaseArtifactService service = new InMemoryArtifactService(); // Or GcsArtifactService](#__codelineno-27-76)[// MyArtifactLoaderService loader = new MyArtifactLoaderService(service, "myJavaApp");](#__codelineno-27-77)[// loader.processLatestReportJava("user123", "sessionABC", "java_report.pdf");](#__codelineno-27-78)[// Due to async nature, in a real app, ensure program waits or handles completion.](#__codelineno-27-79)[}](#__codelineno-27-80)[}](#__codelineno-27-81)

#### Listing Artifact Filenames[¶](#listing-artifact-filenames)

-
**Code Example:**[from google.adk.tools.tool_context import ToolContext](#__codelineno-28-1)[def list_user_files_py(tool_context: ToolContext) -> str:](#__codelineno-28-3)["""Tool to list available artifacts for the user."""](#__codelineno-28-4)[try:](#__codelineno-28-5)[available_files = await tool_context.list_artifacts()](#__codelineno-28-6)[if not available_files:](#__codelineno-28-7)[return "You have no saved artifacts."](#__codelineno-28-8)[else:](#__codelineno-28-9)[# Format the list for the user/LLM](#__codelineno-28-10)[file_list_str = "\n".join([f"- {fname}" for fname in available_files])](#__codelineno-28-11)[return f"Here are your available Python artifacts:\n{file_list_str}"](#__codelineno-28-12)[except ValueError as e:](#__codelineno-28-13)[print(f"Error listing Python artifacts: {e}. Is ArtifactService configured?")](#__codelineno-28-14)[return "Error: Could not list Python artifacts."](#__codelineno-28-15)[except Exception as e:](#__codelineno-28-16)[print(f"An unexpected error occurred during Python artifact list: {e}")](#__codelineno-28-17)[return "Error: An unexpected error occurred while listing Python artifacts."](#__codelineno-28-18)[# This function would typically be wrapped in a FunctionTool](#__codelineno-28-20)[# from google.adk.tools import FunctionTool](#__codelineno-28-21)[# list_files_tool = FunctionTool(func=list_user_files_py)](#__codelineno-28-22)[import { ToolContext } from '@google/adk';](#__codelineno-29-1)[async function listUserFiles(toolContext: ToolContext): Promise<string> {](#__codelineno-29-3)[/**Tool to list available artifacts for the user.*/](#__codelineno-29-4)[try {](#__codelineno-29-5)[const availableFiles = await toolContext.listArtifacts();](#__codelineno-29-6)[if (!availableFiles || availableFiles.length === 0) {](#__codelineno-29-7)[return "You have no saved artifacts.";](#__codelineno-29-8)[} else {](#__codelineno-29-9)[// Format the list for the user/LLM](#__codelineno-29-10)[const fileListStr = availableFiles.map(fname => `- ${fname}`).join("\n");](#__codelineno-29-11)[return `Here are your available TypeScript artifacts:\n${fileListStr}`;](#__codelineno-29-12)[}](#__codelineno-29-13)[} catch (e: any) {](#__codelineno-29-14)[console.error(`Error listing TypeScript artifacts: ${e.message}. Is ArtifactService configured?`);](#__codelineno-29-15)[return "Error: Could not list TypeScript artifacts.";](#__codelineno-29-16)[}](#__codelineno-29-17)[}](#__codelineno-29-18)[import (](#__codelineno-30-1)["fmt"](#__codelineno-30-2)["log"](#__codelineno-30-3)["strings"](#__codelineno-30-4)["google.golang.org/adk/agent"](#__codelineno-30-6)["google.golang.org/adk/llm"](#__codelineno-30-7)["google.golang.org/genai"](#__codelineno-30-8)[)](#__codelineno-30-9)[// listUserFilesCallback is a BeforeModel callback that lists available artifacts](#__codelineno-30-11)[// and adds the list as context to the LLM request.](#__codelineno-30-12)[func listUserFilesCallback(ctx agent.CallbackContext, req *model.LLMRequest) (*model.LLMResponse, error) {](#__codelineno-30-13)[log.Println("[Callback] listUserFilesCallback triggered.")](#__codelineno-30-14)[// List the available artifacts from the artifact service.](#__codelineno-30-15)[listResponse, err := ctx.Artifacts().List(ctx)](#__codelineno-30-16)[if err != nil {](#__codelineno-30-17)[log.Printf("An unexpected error occurred during Go artifact list: %v", err)](#__codelineno-30-18)[return nil, nil // Continue, but log the error.](#__codelineno-30-19)[}](#__codelineno-30-20)[availableFiles := listResponse.FileNames](#__codelineno-30-22)[log.Printf("Found %d available files.", len(availableFiles))](#__codelineno-30-24)[// If there are available files, add them to the LLM request.](#__codelineno-30-26)[if len(availableFiles) > 0 {](#__codelineno-30-27)[var fileListStr strings.Builder](#__codelineno-30-28)[fileListStr.WriteString("SYSTEM: The following files are available:\n")](#__codelineno-30-29)[for _, fname := range availableFiles {](#__codelineno-30-30)[fileListStr.WriteString(fmt.Sprintf("- %s\n", fname))](#__codelineno-30-31)[}](#__codelineno-30-32)[// Prepend this information to the user's request for the model.](#__codelineno-30-33)[if len(req.Contents) > 0 {](#__codelineno-30-34)[lastContent := req.Contents[len(req.Contents)-1]](#__codelineno-30-35)[if len(lastContent.Parts) > 0 {](#__codelineno-30-36)[fileListStr.WriteString("\n") // Add a newline for separation.](#__codelineno-30-37)[lastContent.Parts[0] = genai.NewPartFromText(fileListStr.String() + lastContent.Parts[0].Text)](#__codelineno-30-38)[log.Println("Added file list to LLM request context.")](#__codelineno-30-39)[}](#__codelineno-30-40)[}](#__codelineno-30-41)[log.Printf("Available files:\n%s", fileListStr.String())](#__codelineno-30-42)[} else {](#__codelineno-30-43)[log.Println("No available files found to list.")](#__codelineno-30-44)[}](#__codelineno-30-45)[// Return nil to continue to the next callback or the model.](#__codelineno-30-47)[return nil, nil // Continue to next callback or LLM call](#__codelineno-30-48)[}](#__codelineno-30-49)[import com.google.adk.artifacts.BaseArtifactService;](#__codelineno-31-1)[import com.google.adk.artifacts.ListArtifactsResponse;](#__codelineno-31-2)[import com.google.common.collect.ImmutableList;](#__codelineno-31-3)[import io.reactivex.rxjava3.core.SingleObserver;](#__codelineno-31-4)[import io.reactivex.rxjava3.disposables.Disposable;](#__codelineno-31-5)[public class MyArtifactListerService {](#__codelineno-31-7)[private final BaseArtifactService artifactService;](#__codelineno-31-9)[private final String appName;](#__codelineno-31-10)[public MyArtifactListerService(BaseArtifactService artifactService, String appName) {](#__codelineno-31-12)[this.artifactService = artifactService;](#__codelineno-31-13)[this.appName = appName;](#__codelineno-31-14)[}](#__codelineno-31-15)[// Example method that might be called by a tool or agent logic](#__codelineno-31-17)[public void listUserFilesJava(String userId, String sessionId) {](#__codelineno-31-18)[artifactService](#__codelineno-31-19)[.listArtifactKeys(appName, userId, sessionId)](#__codelineno-31-20)[.subscribe(](#__codelineno-31-21)[new SingleObserver<ListArtifactsResponse>() {](#__codelineno-31-22)[@Override](#__codelineno-31-23)[public void onSubscribe(Disposable d) {](#__codelineno-31-24)[// Optional: handle subscription](#__codelineno-31-25)[}](#__codelineno-31-26)[@Override](#__codelineno-31-28)[public void onSuccess(ListArtifactsResponse response) {](#__codelineno-31-29)[ImmutableList<String> availableFiles = response.filenames();](#__codelineno-31-30)[if (availableFiles.isEmpty()) {](#__codelineno-31-31)[System.out.println(](#__codelineno-31-32)["User "](#__codelineno-31-33)[+ userId](#__codelineno-31-34)[+ " in session "](#__codelineno-31-35)[+ sessionId](#__codelineno-31-36)[+ " has no saved Java artifacts.");](#__codelineno-31-37)[} else {](#__codelineno-31-38)[StringBuilder fileListStr =](#__codelineno-31-39)[new StringBuilder(](#__codelineno-31-40)["Here are the available Java artifacts for user "](#__codelineno-31-41)[+ userId](#__codelineno-31-42)[+ " in session "](#__codelineno-31-43)[+ sessionId](#__codelineno-31-44)[+ ":\n");](#__codelineno-31-45)[for (String fname : availableFiles) {](#__codelineno-31-46)[fileListStr.append("- ").append(fname).append("\n");](#__codelineno-31-47)[}](#__codelineno-31-48)[System.out.println(fileListStr.toString());](#__codelineno-31-49)[}](#__codelineno-31-50)[}](#__codelineno-31-51)[@Override](#__codelineno-31-53)[public void onError(Throwable e) {](#__codelineno-31-54)[System.err.println(](#__codelineno-31-55)["Error listing Java artifacts for user "](#__codelineno-31-56)[+ userId](#__codelineno-31-57)[+ " in session "](#__codelineno-31-58)[+ sessionId](#__codelineno-31-59)[+ ": "](#__codelineno-31-60)[+ e.getMessage());](#__codelineno-31-61)[// In a real application, you might return an error message to the user/LLM](#__codelineno-31-62)[}](#__codelineno-31-63)[});](#__codelineno-31-64)[}](#__codelineno-31-65)[// --- Example Usage Concept (Java) ---](#__codelineno-31-67)[public static void main(String[] args) {](#__codelineno-31-68)[// BaseArtifactService service = new InMemoryArtifactService(); // Or GcsArtifactService](#__codelineno-31-69)[// MyArtifactListerService lister = new MyArtifactListerService(service, "myJavaApp");](#__codelineno-31-70)[// lister.listUserFilesJava("user123", "sessionABC");](#__codelineno-31-71)[// Due to async nature, in a real app, ensure program waits or handles completion.](#__codelineno-31-72)[}](#__codelineno-31-73)[}](#__codelineno-31-74)

These methods for saving, loading, and listing provide a convenient and consistent way to manage binary data persistence within ADK, whether using Python's context objects or directly interacting with the `BaseArtifactService`

in Java, regardless of the chosen backend storage implementation.

## Available Implementations[¶](#available-implementations)

ADK provides concrete implementations of the `BaseArtifactService`

interface, offering different storage backends suitable for various development stages and deployment needs. These implementations handle the details of storing, versioning, and retrieving artifact data based on the `app_name`

, `user_id`

, `session_id`

, and `filename`

(including the `user:`

namespace prefix).

### InMemoryArtifactService[¶](#inmemoryartifactservice)

**Storage Mechanism:**- Python: Uses a Python dictionary (
`self.artifacts`

) held in the application's memory. The dictionary keys represent the artifact path, and the values are lists of`types.Part`

, where each list element is a version. - Java: Uses nested
`HashMap`

instances (`private final Map<String, Map<String, Map<String, Map<String, List<Part>>>>> artifacts;`

) held in memory. The keys at each level are`appName`

,`userId`

,`sessionId`

, and`filename`

respectively. The innermost`List<Part>`

stores the versions of the artifact, where the list index corresponds to the version number.

- Python: Uses a Python dictionary (
**Key Features:****Simplicity:**Requires no external setup or dependencies beyond the core ADK library.**Speed:**Operations are typically very fast as they involve in-memory map/dictionary lookups and list manipulations.**Ephemeral:**All stored artifacts are**lost**when the application process terminates. Data does not persist between application restarts.

**Use Cases:**- Ideal for local development and testing where persistence is not required.
- Suitable for short-lived demonstrations or scenarios where artifact data is purely temporary within a single run of the application.

-
**Instantiation:**[import { InMemoryArtifactService } from '@google/adk';](#__codelineno-33-1)[// Simply instantiate the class](#__codelineno-33-3)[const inMemoryService = new InMemoryArtifactService();](#__codelineno-33-4)[// This instance would then be provided to your Runner.](#__codelineno-33-6)[// const runner = new InMemoryRunner({](#__codelineno-33-7)[// /* other services */,](#__codelineno-33-8)[// artifactService: inMemoryService](#__codelineno-33-9)[// });](#__codelineno-33-10)[import (](#__codelineno-34-1)["google.golang.org/adk/artifactservice"](#__codelineno-34-2)[)](#__codelineno-34-3)[// Simply instantiate the service](#__codelineno-34-5)[artifactService := artifact.InMemoryService()](#__codelineno-34-6)[log.Printf("InMemoryArtifactService (Go) instantiated: %T", artifactService)](#__codelineno-34-7)[// Use the service in your runner](#__codelineno-34-9)[// r, _ := runner.New(runner.Config{](#__codelineno-34-10)[// Agent: agent,](#__codelineno-34-11)[// AppName: "my_app",](#__codelineno-34-12)[// SessionService: sessionService,](#__codelineno-34-13)[// ArtifactService: artifactService,](#__codelineno-34-14)[// })](#__codelineno-34-15)[import com.google.adk.artifacts.BaseArtifactService;](#__codelineno-35-1)[import com.google.adk.artifacts.InMemoryArtifactService;](#__codelineno-35-2)[public class InMemoryServiceSetup {](#__codelineno-35-4)[public static void main(String[] args) {](#__codelineno-35-5)[// Simply instantiate the class](#__codelineno-35-6)[BaseArtifactService inMemoryServiceJava = new InMemoryArtifactService();](#__codelineno-35-7)[System.out.println("InMemoryArtifactService (Java) instantiated: " + inMemoryServiceJava.getClass().getName());](#__codelineno-35-9)[// This instance would then be provided to your Runner.](#__codelineno-35-11)[// Runner runner = new Runner(](#__codelineno-35-12)[// /* other services */,](#__codelineno-35-13)[// inMemoryServiceJava](#__codelineno-35-14)[// );](#__codelineno-35-15)[}](#__codelineno-35-16)[}](#__codelineno-35-17)

### GcsArtifactService[¶](#gcsartifactservice)

**Storage Mechanism:**Leverages Google Cloud Storage (GCS) for persistent artifact storage. Each version of an artifact is stored as a separate object (blob) within a specified GCS bucket.**Object Naming Convention:**It constructs GCS object names (blob names) using a hierarchical path structure.**Key Features:****Persistence:**Artifacts stored in GCS persist across application restarts and deployments.**Scalability:**Leverages the scalability and durability of Google Cloud Storage.**Versioning:**Explicitly stores each version as a distinct GCS object. The`saveArtifact`

method in`GcsArtifactService`

.**Permissions Required:**The application environment needs appropriate credentials (e.g., Application Default Credentials) and IAM permissions to read from and write to the specified GCS bucket.

**Use Cases:**- Production environments requiring persistent artifact storage.
- Scenarios where artifacts need to be shared across different application instances or services (by accessing the same GCS bucket).
- Applications needing long-term storage and retrieval of user or session data.

-
**Instantiation:**[from google.adk.artifacts import GcsArtifactService](#__codelineno-36-1)[# Specify the GCS bucket name](#__codelineno-36-3)[gcs_bucket_name_py = "your-gcs-bucket-for-adk-artifacts" # Replace with your bucket name](#__codelineno-36-4)[try:](#__codelineno-36-6)[gcs_service_py = GcsArtifactService(bucket_name=gcs_bucket_name_py)](#__codelineno-36-7)[print(f"Python GcsArtifactService initialized for bucket: {gcs_bucket_name_py}")](#__codelineno-36-8)[# Ensure your environment has credentials to access this bucket.](#__codelineno-36-9)[# e.g., via Application Default Credentials (ADC)](#__codelineno-36-10)[# Then pass it to the Runner](#__codelineno-36-12)[# runner = Runner(..., artifact_service=gcs_service_py)](#__codelineno-36-13)[except Exception as e:](#__codelineno-36-15)[# Catch potential errors during GCS client initialization (e.g., auth issues)](#__codelineno-36-16)[print(f"Error initializing Python GcsArtifactService: {e}")](#__codelineno-36-17)[# Handle the error appropriately - maybe fall back to InMemory or raise](#__codelineno-36-18)[import com.google.adk.artifacts.BaseArtifactService;](#__codelineno-37-1)[import com.google.adk.artifacts.GcsArtifactService;](#__codelineno-37-2)[import com.google.cloud.storage.Storage;](#__codelineno-37-3)[import com.google.cloud.storage.StorageOptions;](#__codelineno-37-4)[public class GcsServiceSetup {](#__codelineno-37-6)[public static void main(String[] args) {](#__codelineno-37-7)[// Specify the GCS bucket name](#__codelineno-37-8)[String gcsBucketNameJava = "your-gcs-bucket-for-adk-artifacts"; // Replace with your bucket name](#__codelineno-37-9)[try {](#__codelineno-37-11)[// Initialize the GCS Storage client.](#__codelineno-37-12)[// This will use Application Default Credentials by default.](#__codelineno-37-13)[// Ensure the environment is configured correctly (e.g., GOOGLE_APPLICATION_CREDENTIALS).](#__codelineno-37-14)[Storage storageClient = StorageOptions.getDefaultInstance().getService();](#__codelineno-37-15)[// Instantiate the GcsArtifactService](#__codelineno-37-17)[BaseArtifactService gcsServiceJava =](#__codelineno-37-18)[new GcsArtifactService(gcsBucketNameJava, storageClient);](#__codelineno-37-19)[System.out.println(](#__codelineno-37-21)["Java GcsArtifactService initialized for bucket: " + gcsBucketNameJava);](#__codelineno-37-22)[// This instance would then be provided to your Runner.](#__codelineno-37-24)[// Runner runner = new Runner(](#__codelineno-37-25)[// /* other services */,](#__codelineno-37-26)[// gcsServiceJava](#__codelineno-37-27)[// );](#__codelineno-37-28)[} catch (Exception e) {](#__codelineno-37-30)[// Catch potential errors during GCS client initialization (e.g., auth, permissions)](#__codelineno-37-31)[System.err.println("Error initializing Java GcsArtifactService: " + e.getMessage());](#__codelineno-37-32)[e.printStackTrace();](#__codelineno-37-33)[// Handle the error appropriately](#__codelineno-37-34)[}](#__codelineno-37-35)[}](#__codelineno-37-36)[}](#__codelineno-37-37)

Choosing the appropriate `ArtifactService`

implementation depends on your application's requirements for data persistence, scalability, and operational environment.

## Best Practices[¶](#best-practices)

To use artifacts effectively and maintainably:

**Choose the Right Service:**Use`InMemoryArtifactService`

for rapid prototyping, testing, and scenarios where persistence isn't needed. Use`GcsArtifactService`

(or implement your own`BaseArtifactService`

for other backends) for production environments requiring data persistence and scalability.**Meaningful Filenames:**Use clear, descriptive filenames. Including relevant extensions (`.pdf`

,`.png`

,`.wav`

) helps humans understand the content, even though the`mime_type`

dictates programmatic handling. Establish conventions for temporary vs. persistent artifact names.**Specify Correct MIME Types:**Always provide an accurate`mime_type`

when creating the`types.Part`

for`save_artifact`

. This is critical for applications or tools that later`load_artifact`

to interpret the`bytes`

data correctly. Use standard IANA MIME types where possible.**Understand Versioning:**Remember that`load_artifact()`

without a specific`version`

argument retrieves the*latest*version. If your logic depends on a specific historical version of an artifact, be sure to provide the integer version number when loading.**Use Namespacing (**Only use the`user:`

) Deliberately:`"user:"`

prefix for filenames when the data truly belongs to the user and should be accessible across all their sessions. For data specific to a single conversation or session, use regular filenames without the prefix.**Error Handling:**- Always check if an
`artifact_service`

is actually configured before calling context methods (`save_artifact`

,`load_artifact`

,`list_artifacts`

) – they will raise a`ValueError`

if the service is`None`

. - Check the return value of
`load_artifact`

, as it will be`None`

if the artifact or version doesn't exist. Don't assume it always returns a`Part`

. - Be prepared to handle exceptions from the underlying storage service, especially with
`GcsArtifactService`

(e.g.,`google.api_core.exceptions.Forbidden`

for permission issues,`NotFound`

if the bucket doesn't exist, network errors).

- Always check if an
**Size Considerations:**Artifacts are suitable for typical file sizes, but be mindful of potential costs and performance impacts with extremely large files, especially with cloud storage.`InMemoryArtifactService`

can consume significant memory if storing many large artifacts. Evaluate if very large data might be better handled through direct GCS links or other specialized storage solutions rather than passing entire byte arrays in-memory.**Cleanup Strategy:**For persistent storage like`GcsArtifactService`

, artifacts remain until explicitly deleted. If artifacts represent temporary data or have a limited lifespan, implement a strategy for cleanup. This might involve:- Using GCS lifecycle policies on the bucket.
- Building specific tools or administrative functions that utilize the
`artifact_service.delete_artifact`

method (note: delete is*not*exposed via context objects for safety). - Carefully managing filenames to allow pattern-based deletion if needed.