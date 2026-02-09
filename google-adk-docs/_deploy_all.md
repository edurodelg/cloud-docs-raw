---
merged_at: 2026-02-09T09:31:35.508056
merged_files: 4
---


---
<!-- Source: https://google.github.io/adk-docs/deploy/ -->

# Deploying Your Agent¶

# Deploying Your Agent[¶](#deploying-your-agent)

Once you've built and tested your agent using ADK, the next step is to deploy it so it can be accessed, queried, and used in production or integrated with other applications. Deployment moves your agent from your local development machine to a scalable and reliable environment.

## Deployment Options[¶](#deployment-options)

Your ADK agent can be deployed to a range of different environments based on your needs for production readiness or custom flexibility:

### Agent Engine in Vertex AI[¶](#agent-engine-in-vertex-ai)

[Agent Engine](agent-engine/) is a fully managed auto-scaling service on Google Cloud
specifically designed for deploying, managing, and scaling AI agents built with
frameworks such as ADK.

Learn more about [deploying your agent to Vertex AI Agent Engine](agent-engine/).

### Cloud Run[¶](#cloud-run)

[Cloud Run](https://cloud.google.com/run) is a managed auto-scaling compute platform on
Google Cloud that enables you to run your agent as a container-based
application.

Learn more about [deploying your agent to Cloud Run](cloud-run/).

### Google Kubernetes Engine (GKE)[¶](#google-kubernetes-engine-gke)

[Google Kubernetes Engine (GKE)](https://cloud.google.com/kubernetes-engine) is a managed
Kubernetes service of Google Cloud that allows you to run your agent in a containerized
environment. GKE is a good option if you need more control over the deployment as well as
for running Open Models.

Learn more about [deploying your agent to GKE](gke/).

### Other Container-friendly Infrastructure[¶](#other-container-friendly-infrastructure)

You can manually package your Agent into a container image and then run it in any environment that supports container images. For example you can run it locally in Docker or Podman. This is a good option if you prefer to run offline or disconnected, or otherwise in a system that has no connection to Google Cloud.

Follow the instructions for [deploying your agent to Cloud Run](cloud-run/#deployment-commands).
In the "Deployment Commands" section for gcloud CLI, you will find an example FastAPI entry point and
Dockerfile.

---
<!-- Source: https://google.github.io/adk-docs/deploy/gke/ -->

# Deploy to Google Kubernetes Engine (GKE)¶

# Deploy to Google Kubernetes Engine (GKE)[¶](#deploy-to-google-kubernetes-engine-gke)

[GKE](https://cloud.google.com/gke) is the Google Cloud managed Kubernetes service. It allows you to deploy and manage containerized applications using Kubernetes.

To deploy your agent you will need to have a Kubernetes cluster running on GKE. You can create a cluster using the Google Cloud Console or the `gcloud`

command line tool.

In this example we will deploy a simple agent to GKE. The agent will be a FastAPI application that uses `Gemini 2.0 Flash`

as the LLM. We can use Vertex AI or AI Studio as the LLM provider using the Environment variable `GOOGLE_GENAI_USE_VERTEXAI`

.

## Environment variables[¶](#environment-variables)

Set your environment variables as described in the [Setup and Installation](../../get-started/installation/) guide. You also need to install the `kubectl`

command line tool. You can find instructions to do so in the [Google Kubernetes Engine Documentation](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl).

export GOOGLE_CLOUD_PROJECT=your-project-id # Your GCP project ID
export GOOGLE_CLOUD_LOCATION=us-central1 # Or your preferred location
export GOOGLE_GENAI_USE_VERTEXAI=true # Set to true if using Vertex AI
export GOOGLE_CLOUD_PROJECT_NUMBER=$(gcloud projects describe --format json $GOOGLE_CLOUD_PROJECT | jq -r ".projectNumber")


If you don't have `jq`

installed, you can use the following command to get the project number:

And copy the project number from the output.

## Enable APIs and Permissions[¶](#enable-apis-and-permissions)

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

Enable the necessary APIs for your project. You can do this using the `gcloud`

command line tool.

gcloud services enable \
container.googleapis.com \
artifactregistry.googleapis.com \
cloudbuild.googleapis.com \
aiplatform.googleapis.com


Grant necessary roles to the default compute engine service account required by the `gcloud builds submit`

command.

ROLES_TO_ASSIGN=(
"roles/artifactregistry.writer"
"roles/storage.objectViewer"
"roles/logging.viewer"
"roles/logging.logWriter"
)
for ROLE in "${ROLES_TO_ASSIGN[@]}"; do
gcloud projects add-iam-policy-binding "${GOOGLE_CLOUD_PROJECT}" \
--member="serviceAccount:${GOOGLE_CLOUD_PROJECT_NUMBER}-compute@developer.gserviceaccount.com" \
--role="${ROLE}"
done


## Deployment payload[¶](#payload)

When you deploy your ADK agent workflow to the Google Cloud GKE, the following content is uploaded to the service:

- Your ADK agent code
- Any dependencies declared in your ADK agent code
- ADK API server code version used by your agent

The default deployment *does not* include the ADK web user interface libraries,
unless you specify it as deployment setting, such as the `--with_ui`

option for
`adk deploy gke`

command.

## Deployment options[¶](#deployment-options)

You can deploy your agent to GKE either **manually using Kubernetes manifests** or **automatically using the adk deploy gke command**. Choose the approach that best suits your workflow.

## Option 1: Manual Deployment using gcloud and kubectl[¶](#option-1-manual-deployment-using-gcloud-and-kubectl)

### Create a GKE cluster[¶](#create-a-gke-cluster)

You can create a GKE cluster using the `gcloud`

command line tool. This example creates an Autopilot cluster named `adk-cluster`

in the `us-central1`

region.

If creating a GKE Standard cluster, make sure

[Workload Identity]is enabled. Workload Identity is enabled by default in an AutoPilot cluster.

gcloud container clusters create-auto adk-cluster \
--location=$GOOGLE_CLOUD_LOCATION \
--project=$GOOGLE_CLOUD_PROJECT


After creating the cluster, you need to connect to it using `kubectl`

. This command configures `kubectl`

to use the credentials for your new cluster.

gcloud container clusters get-credentials adk-cluster \
--location=$GOOGLE_CLOUD_LOCATION \
--project=$GOOGLE_CLOUD_PROJECT


### Create Your Agent[¶](#create-your-agent)

We will reference the `capital_agent`

example defined on the [LLM agents](../../agents/llm-agents/) page.

To proceed, organize your project files as follows:

your-project-directory/
├── capital_agent/
│ ├── __init__.py
│ └── agent.py # Your agent code (see "Capital Agent example" below)
├── main.py # FastAPI application entry point
├── requirements.txt # Python dependencies
└── Dockerfile # Container build instructions


### Code files[¶](#code-files)

Create the following files (`main.py`

, `requirements.txt`

, `Dockerfile`

, `capital_agent/agent.py`

, `capital_agent/__init__.py`

) in the root of `your-project-directory/`

.

-
This is the Capital Agent example inside the

`capital_agent`

directorycapital_agent/agent.py[from google.adk.agents import LlmAgent](#__codelineno-8-1)[# Define a tool function](#__codelineno-8-3)[def get_capital_city(country: str) -> str:](#__codelineno-8-4)["""Retrieves the capital city for a given country."""](#__codelineno-8-5)[# Replace with actual logic (e.g., API call, database lookup)](#__codelineno-8-6)[capitals = {"france": "Paris", "japan": "Tokyo", "canada": "Ottawa"}](#__codelineno-8-7)[return capitals.get(country.lower(), f"Sorry, I don't know the capital of {country}.")](#__codelineno-8-8)[# Add the tool to the agent](#__codelineno-8-10)[capital_agent = LlmAgent(](#__codelineno-8-11)[model="gemini-2.0-flash",](#__codelineno-8-12)[name="capital_agent", #name of your agent](#__codelineno-8-13)[description="Answers user questions about the capital city of a given country.",](#__codelineno-8-14)[instruction="""You are an agent that provides the capital city of a country... (previous instruction text)""",](#__codelineno-8-15)[tools=[get_capital_city] # Provide the function directly](#__codelineno-8-16)[)](#__codelineno-8-17)[# ADK will discover the root_agent instance](#__codelineno-8-19)[root_agent = capital_agent](#__codelineno-8-20)Mark your directory as a python package

-
This file sets up the FastAPI application using

`get_fast_api_app()`

from ADK:main.py[import os](#__codelineno-10-1)[import uvicorn](#__codelineno-10-3)[from fastapi import FastAPI](#__codelineno-10-4)[from google.adk.cli.fast_api import get_fast_api_app](#__codelineno-10-5)[# Get the directory where main.py is located](#__codelineno-10-7)[AGENT_DIR = os.path.dirname(os.path.abspath(__file__))](#__codelineno-10-8)[# Example session service URI (e.g., SQLite)](#__codelineno-10-9)[# Note: Use 'sqlite+aiosqlite' instead of 'sqlite' because DatabaseSessionService requires an async driver](#__codelineno-10-10)[SESSION_SERVICE_URI = "sqlite+aiosqlite:///./sessions.db"](#__codelineno-10-11)[# Example allowed origins for CORS](#__codelineno-10-12)[ALLOWED_ORIGINS = ["http://localhost", "http://localhost:8080", "*"]](#__codelineno-10-13)[# Set web=True if you intend to serve a web interface, False otherwise](#__codelineno-10-14)[SERVE_WEB_INTERFACE = True](#__codelineno-10-15)[# Call the function to get the FastAPI app instance](#__codelineno-10-17)[# Ensure the agent directory name ('capital_agent') matches your agent folder](#__codelineno-10-18)[app: FastAPI = get_fast_api_app(](#__codelineno-10-19)[agents_dir=AGENT_DIR,](#__codelineno-10-20)[session_service_uri=SESSION_SERVICE_URI,](#__codelineno-10-21)[allow_origins=ALLOWED_ORIGINS,](#__codelineno-10-22)[web=SERVE_WEB_INTERFACE,](#__codelineno-10-23)[)](#__codelineno-10-24)[# You can add more FastAPI routes or configurations below if needed](#__codelineno-10-26)[# Example:](#__codelineno-10-27)[# @app.get("/hello")](#__codelineno-10-28)[# async def read_root():](#__codelineno-10-29)[# return {"Hello": "World"}](#__codelineno-10-30)[if __name__ == "__main__":](#__codelineno-10-32)[# Use the PORT environment variable provided by Cloud Run, defaulting to 8080](#__codelineno-10-33)[uvicorn.run(app, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))](#__codelineno-10-34)*Note: We specify*`agent_dir`

to the directory`main.py`

is in and use`os.environ.get("PORT", 8080)`

for Cloud Run compatibility. -
List the necessary Python packages:

-
Define the container image:

Dockerfile[FROM python:3.13-slim](#__codelineno-12-1)[WORKDIR /app](#__codelineno-12-2)[COPY requirements.txt .](#__codelineno-12-4)[RUN pip install --no-cache-dir -r requirements.txt](#__codelineno-12-5)[RUN adduser --disabled-password --gecos "" myuser && \](#__codelineno-12-7)[chown -R myuser:myuser /app](#__codelineno-12-8)[COPY . .](#__codelineno-12-10)[USER myuser](#__codelineno-12-12)[ENV PATH="/home/myuser/.local/bin:$PATH"](#__codelineno-12-14)[CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port $PORT"]](#__codelineno-12-16)

### Build the container image[¶](#build-the-container-image)

You need to create a Google Artifact Registry repository to store your container images. You can do this using the `gcloud`

command line tool.

gcloud artifacts repositories create adk-repo \
--repository-format=docker \
--location=$GOOGLE_CLOUD_LOCATION \
--description="ADK repository"


Build the container image using the `gcloud`

command line tool. This example builds the image and tags it as `adk-repo/adk-agent:latest`

.

gcloud builds submit \
--tag $GOOGLE_CLOUD_LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/adk-repo/adk-agent:latest \
--project=$GOOGLE_CLOUD_PROJECT \
.


Verify the image is built and pushed to the Artifact Registry:

gcloud artifacts docker images list \
$GOOGLE_CLOUD_LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/adk-repo \
--project=$GOOGLE_CLOUD_PROJECT


### Configure Kubernetes Service Account for Vertex AI[¶](#configure-kubernetes-service-account-for-vertex-ai)

If your agent uses Vertex AI, you need to create a Kubernetes service account with the necessary permissions. This example creates a service account named `adk-agent-sa`

and binds it to the `Vertex AI User`

role.

If you are using AI Studio and accessing the model with an API key you can skip this step.


gcloud projects add-iam-policy-binding projects/${GOOGLE_CLOUD_PROJECT} \
--role=roles/aiplatform.user \
--member=principal://iam.googleapis.com/projects/${GOOGLE_CLOUD_PROJECT_NUMBER}/locations/global/workloadIdentityPools/${GOOGLE_CLOUD_PROJECT}.svc.id.goog/subject/ns/default/sa/adk-agent-sa \
--condition=None


### Create the Kubernetes manifest files[¶](#create-the-kubernetes-manifest-files)

Create a Kubernetes deployment manifest file named `deployment.yaml`

in your project directory. This file defines how to deploy your application on GKE.

cat << EOF > deployment.yaml
apiVersion: apps/v1
kind: Deployment
metadata:
name: adk-agent
spec:
replicas: 1
selector:
matchLabels:
app: adk-agent
template:
metadata:
labels:
app: adk-agent
spec:
serviceAccount: adk-agent-sa
containers:
- name: adk-agent
imagePullPolicy: Always
image: $GOOGLE_CLOUD_LOCATION-docker.pkg.dev/$GOOGLE_CLOUD_PROJECT/adk-repo/adk-agent:latest
resources:
limits:
memory: "128Mi"
cpu: "500m"
ephemeral-storage: "128Mi"
requests:
memory: "128Mi"
cpu: "500m"
ephemeral-storage: "128Mi"
ports:
- containerPort: 8080
env:
- name: PORT
value: "8080"
- name: GOOGLE_CLOUD_PROJECT
value: $GOOGLE_CLOUD_PROJECT
- name: GOOGLE_CLOUD_LOCATION
value: $GOOGLE_CLOUD_LOCATION
- name: GOOGLE_GENAI_USE_VERTEXAI
value: "$GOOGLE_GENAI_USE_VERTEXAI"
# If using AI Studio, set GOOGLE_GENAI_USE_VERTEXAI to false and set the following:
# - name: GOOGLE_API_KEY
# value: $GOOGLE_API_KEY
# Add any other necessary environment variables your agent might need
---
apiVersion: v1
kind: Service
metadata:
name: adk-agent
spec:
type: LoadBalancer
ports:
- port: 80
targetPort: 8080
selector:
app: adk-agent
EOF


### Deploy the Application[¶](#deploy-the-application)

Deploy the application using the `kubectl`

command line tool. This command applies the deployment and service manifest files to your GKE cluster.

After a few moments, you can check the status of your deployment using:

This command lists the pods associated with your deployment. You should see a pod with a status of `Running`

.

Once the pod is running, you can check the status of the service using:

If the output shows a `External IP`

, it means your service is accessible from the internet. It may take a few minutes for the external IP to be assigned.

You can get the external IP address of your service using:

## Option 2: Automated Deployment using `adk deploy gke`

[¶](#option-2-automated-deployment-using-adk-deploy-gke)

ADK provides a CLI command to streamline GKE deployment. This avoids the need to manually build images, write Kubernetes manifests, or push to Artifact Registry.

#### Prerequisites[¶](#prerequisites)

Before you begin, ensure you have the following set up:

-
**A running GKE cluster:**You need an active Kubernetes cluster on Google Cloud. -
**Required CLIs:**The Google Cloud CLI must be installed, authenticated, and configured to use your target project. Run`gcloud`

CLI:`gcloud auth login`

and`gcloud config set project [YOUR_PROJECT_ID]`

.**kubectl:**The Kubernetes CLI must be installed to deploy the application to your cluster.

-
**Enabled Google Cloud APIs:**Make sure the following APIs are enabled in your Google Cloud project:- Kubernetes Engine API (
`container.googleapis.com`

) - Cloud Build API (
`cloudbuild.googleapis.com`

) - Container Registry API (
`containerregistry.googleapis.com`

)

- Kubernetes Engine API (
-
**Required IAM Permissions:**The user or Compute Engine default service account running the command needs, at a minimum, the following roles: -
**Kubernetes Engine Developer**(`roles/container.developer`

): To interact with the GKE cluster. -
**Storage Object Viewer**(`roles/storage.objectViewer`

): To allow Cloud Build to download the source code from the Cloud Storage bucket where gcloud builds submit uploads it. -
**Artifact Registry Create on Push Writer**(`roles/artifactregistry.createOnPushWriter`

): To allow Cloud Build to push the built container image to Artifact Registry. This role also permits the on-the-fly creation of the special gcr.io repository within Artifact Registry if needed on the first push. -
**Logs Writer**(`roles/logging.logWriter`

): To allow Cloud Build to write build logs to Cloud Logging.

### The `deploy gke`

Command[¶](#the-deploy-gke-command)

The command takes the path to your agent and parameters specifying the target GKE cluster.

#### Syntax[¶](#syntax)

### Arguments & Options[¶](#arguments-options)

| Argument | Description | Required |
|---|---|---|
| AGENT_PATH | The local file path to your agent's root directory. | Yes |
| --project | The Google Cloud Project ID where your GKE cluster is located. | Yes |
| --cluster_name | The name of your GKE cluster. | Yes |
| --region | The Google Cloud region of your cluster (e.g., us-central1). | Yes |
| --with_ui | Deploys both the agent's back-end API and a companion front-end user interface. | No |
| --log_level | Sets the logging level for the deployment process. Options: debug, info, warning, error. | No |

### How It Works[¶](#how-it-works)

When you run the `adk deploy gke`

command, the ADK performs the following steps automatically:

-
Containerization: It builds a Docker container image from your agent's source code.

-
Image Push: It tags the container image and pushes it to your project's Artifact Registry.

-
Manifest Generation: It dynamically generates the necessary Kubernetes manifest files (a

`Deployment`

and a`Service`

). -
Cluster Deployment: It applies these manifests to your specified GKE cluster, which triggers the following:


The `Deployment`

instructs GKE to pull the container image from Artifact Registry and run it in one or more Pods.

The `Service`

creates a stable network endpoint for your agent. By default, this is a LoadBalancer service, which provisions a public IP address to expose your agent to the internet.

### Example Usage[¶](#example-usage)

Here is a practical example of deploying an agent located at `~/agents/multi_tool_agent/`

to a GKE cluster named test.

adk deploy gke \
--project myproject \
--cluster_name test \
--region us-central1 \
--with_ui \
--log_level info \
~/agents/multi_tool_agent/


### Verifying Your Deployment[¶](#verifying-your-deployment)

If you used `adk deploy gke`

, verify the deployment using `kubectl`

:

- Check the Pods: Ensure your agent's pods are in the Running state.

`adk-default-service-name-xxxx-xxxx ... 1/1 Running`

in the default namespace.
- Find the External IP: Get the public IP address for your agent's service.

kubectl get service
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
adk-default-service-name LoadBalancer 34.118.228.70 34.63.153.253 80:32581/TCP 5d20h


We can navigate to the external IP and interact with the agent via UI

## Testing your agent[¶](#testing-your-agent)

Once your agent is deployed to GKE, you can interact with it via the deployed UI (if enabled) or directly with its API endpoints using tools like `curl`

. You'll need the service URL provided after deployment.

### UI Testing[¶](#ui-testing)

If you deployed your agent with the UI enabled:

You can test your agent by simply navigating to the kubernetes service URL in your web browser.

The ADK dev UI allows you to interact with your agent, manage sessions, and view execution details directly in the browser.

To verify your agent is working as intended, you can:

- Select your agent from the dropdown menu.
- Type a message and verify that you receive an expected response from your agent.

If you experience any unexpected behavior, check the pod logs for your agent using:

### API Testing (curl)[¶](#api-testing-curl)

You can interact with the agent's API endpoints using tools like `curl`

. This is useful for programmatic interaction or if you deployed without the UI.

#### Set the application URL[¶](#set-the-application-url)

Replace the example URL with the actual URL of your deployed Cloud Run service.

#### List available apps[¶](#list-available-apps)

Verify the deployed application name.

*(Adjust the app_name in the following commands based on this output if needed. The default is often the agent directory name, e.g., capital_agent)*.


#### Create or Update a Session[¶](#create-or-update-a-session)

Initialize or update the state for a specific user and session. Replace `capital_agent`

with your actual app name if different. The values `user_123`

and `session_abc`

are example identifiers; you can replace them with your desired user and session IDs.

curl -X POST \
$APP_URL/apps/capital_agent/users/user_123/sessions/session_abc \
-H "Content-Type: application/json" \
-d '{"preferred_language": "English", "visit_count": 5}'


#### Run the Agent[¶](#run-the-agent)

Send a prompt to your agent. Replace `capital_agent`

with your app name and adjust the user/session IDs and prompt as needed.

curl -X POST $APP_URL/run_sse \
-H "Content-Type: application/json" \
-d '{
"app_name": "capital_agent",
"user_id": "user_123",
"session_id": "session_abc",
"new_message": {
"role": "user",
"parts": [{
"text": "What is the capital of Canada?"
}]
},
"streaming": false
}'


- Set
`"streaming": true`

if you want to receive Server-Sent Events (SSE). - The response will contain the agent's execution events, including the final answer.

## Troubleshooting[¶](#troubleshooting)

These are some common issues you might encounter when deploying your agent to GKE:

### 403 Permission Denied for `Gemini 2.0 Flash`

[¶](#403-permission-denied-for-gemini-20-flash)

This usually means that the Kubernetes service account does not have the necessary permission to access the Vertex AI API. Ensure that you have created the service account and bound it to the `Vertex AI User`

role as described in the [Configure Kubernetes Service Account for Vertex AI](#configure-kubernetes-service-account-for-vertex-ai) section. If you are using AI Studio, ensure that you have set the `GOOGLE_API_KEY`

environment variable in the deployment manifest and it is valid.

### 404 or Not Found response[¶](#404-or-not-found-response)

This usually means there is an error in your request. Check the application logs to diagnose the problem.

export POD_NAME=$(kubectl get pod -l app=adk-agent -o jsonpath='{.items[0].metadata.name}')
kubectl logs $POD_NAME


### Attempt to write a readonly database[¶](#attempt-to-write-a-readonly-database)

You might see there is no session id created in the UI and the agent does not respond to any messages. This is usually caused by the SQLite database being read-only. This can happen if you run the agent locally and then create the container image which copies the SQLite database into the container. The database is then read-only in the container.

sqlalchemy.exc.OperationalError: (sqlite3.OperationalError) attempt to write a readonly database
[SQL: UPDATE app_states SET state=?, update_time=CURRENT_TIMESTAMP WHERE app_states.app_name = ?]


To fix this issue, you can either:

Delete the SQLite database file from your local machine before building the container image. This will create a new SQLite database when the container is started.

or (recommended) you can add a `.dockerignore`

file to your project directory to exclude the SQLite database from being copied into the container image.

Build the container image abd deploy the application again.

### Insufficient Permission to Stream Logs `ERROR: (gcloud.builds.submit)`

[¶](#insufficient-permission-to-stream-logs-error-gcloudbuildssubmit)

This error can occur when you don't have sufficient permissions to stream build logs, or your VPC-SC security policy restricts access to the default logs bucket.

To check the progress of the build, follow the link provided in the error message or navigate to the Cloud Build page in the Google Cloud Console.

You can also verify the image was built and pushed to the Artifact Registry using the command under the [Build the container image](#build-the-container-image) section.

### Gemini-2.0-Flash Not Supported in Live Api[¶](#gemini-20-flash-not-supported-in-live-api)

When using the ADK Dev UI for your deployed agent, text-based chat works, but voice (e.g., clicking the microphone button) fail. You might see a `websockets.exceptions.ConnectionClosedError`

in the pod logs indicating that your model is "not supported in the live api".

This error occurs because the agent is configured with a model (like `gemini-2.0-flash`

in the example) that does not support the Gemini Live API. The Live API is required for real-time, bidirectional streaming of audio and video.

## Cleanup[¶](#cleanup)

To delete the GKE cluster and all associated resources, run:

gcloud container clusters delete adk-cluster \
--location=$GOOGLE_CLOUD_LOCATION \
--project=$GOOGLE_CLOUD_PROJECT


To delete the Artifact Registry repository, run:

gcloud artifacts repositories delete adk-repo \
--location=$GOOGLE_CLOUD_LOCATION \
--project=$GOOGLE_CLOUD_PROJECT


You can also delete the project if you no longer need it. This will delete all resources associated with the project, including the GKE cluster, Artifact Registry repository, and any other resources you created.

---
<!-- Source: https://google.github.io/adk-docs/deploy/cloud-run/ -->

# Deploy to Cloud Run¶

# Deploy to Cloud Run[¶](#deploy-to-cloud-run)

[Cloud Run](https://cloud.google.com/run)
is a fully managed platform that enables you to run your code directly on top of Google's scalable infrastructure.

To deploy your agent, you can use either the `adk deploy cloud_run`

command *(recommended for Python)*, or with `gcloud run deploy`

command through Cloud Run.

## Agent sample[¶](#agent-sample)

For each of the commands, we will reference the `Capital Agent`

sample defined on the [LLM agent](../../agents/llm-agents/) page. We will assume it's in a directory (eg: `capital_agent`

).

To proceed, confirm that your agent code is configured as follows:

- Agent code is in a file called
`agent.py`

within your agent directory. - Your agent variable is named
`root_agent`

. `__init__.py`

is within your agent directory and contains`from . import agent`

.- Your
`requirements.txt`

file is present in the agent directory.

- Your application's entry point (the main package and main() function) is in a single Go file. Using main.go is a strong convention.
- Your agent instance is passed to a launcher configuration, typically using agent.NewSingleLoader(yourAgent). The adkgo tool uses this launcher to start your agent with the correct services.
- Your go.mod and go.sum files are present in your project directory to manage dependencies.

Refer to the following section for more details. You can also find a [sample app](https://github.com/google/adk-docs/tree/main/examples/go/cloud-run) in the Github repo.

- Agent code is in a file called
`CapitalAgent.java`

within your agent directory. - Your agent variable is global and follows the format
`public static final BaseAgent ROOT_AGENT`

. - Your agent definition is present in a static class method.

Refer to the following section for more details. You can also find a [sample app](https://github.com/google/adk-docs/tree/main/examples/java/cloud-run) in the Github repo.

## Environment variables[¶](#environment-variables)

Set your environment variables as described in the [Setup and Installation](../../get-started/installation/) guide.

export GOOGLE_CLOUD_PROJECT=your-project-id
export GOOGLE_CLOUD_LOCATION=us-central1 # Or your preferred location
export GOOGLE_GENAI_USE_VERTEXAI=True


*(Replace your-project-id with your actual GCP project ID)*

Alternatively you can also use an API key from AI Studio

export GOOGLE_CLOUD_PROJECT=your-project-id
export GOOGLE_CLOUD_LOCATION=us-central1 # Or your preferred location
export GOOGLE_GENAI_USE_VERTEXAI=FALSE
export GOOGLE_API_KEY=your-api-key


*(Replace*

`your-project-id`

with your actual GCP project ID and `your-api-key`

with your actual API key from AI Studio)## Prerequisites[¶](#prerequisites)

- You should have a Google Cloud project. You need to know your:
- Project name (i.e. "my-project")
- Project location (i.e. "us-central1")
- Service account (i.e. "1234567890-compute@developer.gserviceaccount.com")
- GOOGLE_API_KEY


## Secret[¶](#secret)

Please make sure you have created a secret which can be read by your service account.

### Entry for GOOGLE_API_KEY secret[¶](#entry-for-google_api_key-secret)

You can create your secret manually or use CLI:

echo "<<put your GOOGLE_API_KEY here>>" | gcloud secrets create GOOGLE_API_KEY --project=my-project --data-file=-


### Permissions to read[¶](#permissions-to-read)

You should give appropriate permission for you service account to read this secret.

gcloud secrets add-iam-policy-binding GOOGLE_API_KEY --member="serviceAccount:1234567890-compute@developer.gserviceaccount.com" --role="roles/secretmanager.secretAccessor" --project=my-project


## Deployment payload[¶](#payload)

When you deploy your ADK agent workflow to the Google Cloud Run, the following content is uploaded to the service:

- Your ADK agent code
- Any dependencies declared in your ADK agent code
- ADK API server code version used by your agent

The default deployment *does not* include the ADK web user interface libraries,
unless you specify it as deployment setting, such as the `--with_ui`

option for
`adk deploy cloud_run`

command.

## Deployment commands[¶](#deployment-commands)

### adk CLI[¶](#adk-cli)

The `adk deploy cloud_run`

command deploys your agent code to Google Cloud Run.

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

#### Setup environment variables[¶](#setup-environment-variables)

Optional but recommended: Setting environment variables can make the deployment commands cleaner.

# Set your Google Cloud Project ID
export GOOGLE_CLOUD_PROJECT="your-gcp-project-id"
# Set your desired Google Cloud Location
export GOOGLE_CLOUD_LOCATION="us-central1" # Example location
# Set the path to your agent code directory
export AGENT_PATH="./capital_agent" # Assuming capital_agent is in the current directory
# Set a name for your Cloud Run service (optional)
export SERVICE_NAME="capital-agent-service"
# Set an application name (optional)
export APP_NAME="capital_agent_app"


#### Command usage[¶](#command-usage)

##### Minimal command[¶](#minimal-command)

adk deploy cloud_run \
--project=$GOOGLE_CLOUD_PROJECT \
--region=$GOOGLE_CLOUD_LOCATION \
$AGENT_PATH


##### Full command with optional flags[¶](#full-command-with-optional-flags)

adk deploy cloud_run \
--project=$GOOGLE_CLOUD_PROJECT \
--region=$GOOGLE_CLOUD_LOCATION \
--service_name=$SERVICE_NAME \
--app_name=$APP_NAME \
--with_ui \
$AGENT_PATH


##### Arguments[¶](#arguments)

`AGENT_PATH`

: (Required) Positional argument specifying the path to the directory containing your agent's source code (e.g.,`$AGENT_PATH`

in the examples, or`capital_agent/`

). This directory must contain at least an`__init__.py`

and your main agent file (e.g.,`agent.py`

).

##### Options[¶](#options)

`--project TEXT`

: (Required) Your Google Cloud project ID (e.g.,`$GOOGLE_CLOUD_PROJECT`

).`--region TEXT`

: (Required) The Google Cloud location for deployment (e.g.,`$GOOGLE_CLOUD_LOCATION`

,`us-central1`

).`--service_name TEXT`

: (Optional) The name for the Cloud Run service (e.g.,`$SERVICE_NAME`

). Defaults to`adk-default-service-name`

.`--app_name TEXT`

: (Optional) The application name for the ADK API server (e.g.,`$APP_NAME`

). Defaults to the name of the directory specified by`AGENT_PATH`

(e.g.,`capital_agent`

if`AGENT_PATH`

is`./capital_agent`

).`--agent_engine_id TEXT`

: (Optional) If you are using a managed session service via Vertex AI Agent Engine, provide its resource ID here.`--port INTEGER`

: (Optional) The port number the ADK API server will listen on within the container. Defaults to 8000.`--with_ui`

: (Optional) If included, deploys the ADK dev UI alongside the agent API server. By default, only the API server is deployed.`--temp_folder TEXT`

: (Optional) Specifies a directory for storing intermediate files generated during the deployment process. Defaults to a timestamped folder in the system's temporary directory.*(Note: This option is generally not needed unless troubleshooting issues).*`--help`

: Show the help message and exit.

##### Passing gcloud CLI Arguments[¶](#passing-gcloud-cli-arguments)

To pass specific gcloud flags through the `adk deploy cloud_run`

command, use the double-dash separator (`--`

) after the ADK arguments. Any flags (except ADK-managed) following the `--`

will be passed directly to the underlying gcloud command.

###### Syntax Example:[¶](#syntax-example)

###### Example:[¶](#example)

adk deploy cloud_run --project=[PROJECT_ID] --region=[REGION] path/to/my_agent -- --no-allow-unauthenticated --min-instances=2


##### Authenticated access[¶](#authenticated-access)

During the deployment process, you might be prompted: `Allow unauthenticated invocations to [your-service-name] (y/N)?`

.

- Enter
`y`

to allow public access to your agent's API endpoint without authentication. - Enter
`N`

(or press Enter for the default) to require authentication (e.g., using an identity token as shown in the "Testing your agent" section).

Upon successful execution, the command deploys your agent to Cloud Run and provide the URL of the deployed service.

### gcloud CLI for Python[¶](#gcloud-cli-for-python)

Alternatively, you can deploy using the standard `gcloud run deploy`

command with a `Dockerfile`

. This method requires more manual setup compared to the `adk`

command but offers flexibility, particularly if you want to embed your agent within a custom [FastAPI](https://fastapi.tiangolo.com/) application.

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

#### Project Structure[¶](#project-structure)

Organize your project files as follows:

your-project-directory/
├── capital_agent/
│ ├── __init__.py
│ └── agent.py # Your agent code (see "Agent sample" tab)
├── main.py # FastAPI application entry point
├── requirements.txt # Python dependencies
└── Dockerfile # Container build instructions


Create the following files (`main.py`

, `requirements.txt`

, `Dockerfile`

) in the root of `your-project-directory/`

.

#### Code files[¶](#code-files)

-
This file sets up the FastAPI application using

`get_fast_api_app()`

from ADK:main.py[import os](#__codelineno-10-1)[import uvicorn](#__codelineno-10-3)[from fastapi import FastAPI](#__codelineno-10-4)[from google.adk.cli.fast_api import get_fast_api_app](#__codelineno-10-5)[# Get the directory where main.py is located](#__codelineno-10-7)[AGENT_DIR = os.path.dirname(os.path.abspath(__file__))](#__codelineno-10-8)[# Example session service URI (e.g., SQLite)](#__codelineno-10-9)[# Note: Use 'sqlite+aiosqlite' instead of 'sqlite' because DatabaseSessionService requires an async driver](#__codelineno-10-10)[SESSION_SERVICE_URI = "sqlite+aiosqlite:///./sessions.db"](#__codelineno-10-11)[# Example allowed origins for CORS](#__codelineno-10-12)[ALLOWED_ORIGINS = ["http://localhost", "http://localhost:8080", "*"]](#__codelineno-10-13)[# Set web=True if you intend to serve a web interface, False otherwise](#__codelineno-10-14)[SERVE_WEB_INTERFACE = True](#__codelineno-10-15)[# Call the function to get the FastAPI app instance](#__codelineno-10-17)[# Ensure the agent directory name ('capital_agent') matches your agent folder](#__codelineno-10-18)[app: FastAPI = get_fast_api_app(](#__codelineno-10-19)[agents_dir=AGENT_DIR,](#__codelineno-10-20)[session_service_uri=SESSION_SERVICE_URI,](#__codelineno-10-21)[allow_origins=ALLOWED_ORIGINS,](#__codelineno-10-22)[web=SERVE_WEB_INTERFACE,](#__codelineno-10-23)[)](#__codelineno-10-24)[# You can add more FastAPI routes or configurations below if needed](#__codelineno-10-26)[# Example:](#__codelineno-10-27)[# @app.get("/hello")](#__codelineno-10-28)[# async def read_root():](#__codelineno-10-29)[# return {"Hello": "World"}](#__codelineno-10-30)[if __name__ == "__main__":](#__codelineno-10-32)[# Use the PORT environment variable provided by Cloud Run, defaulting to 8080](#__codelineno-10-33)[uvicorn.run(app, host="0.0.0.0", port=int(os.environ.get("PORT", 8080)))](#__codelineno-10-34)*Note: We specify*`agent_dir`

to the directory`main.py`

is in and use`os.environ.get("PORT", 8080)`

for Cloud Run compatibility. -
List the necessary Python packages:

-
Define the container image:

Dockerfile[FROM python:3.13-slim](#__codelineno-12-1)[WORKDIR /app](#__codelineno-12-2)[COPY requirements.txt .](#__codelineno-12-4)[RUN pip install --no-cache-dir -r requirements.txt](#__codelineno-12-5)[RUN adduser --disabled-password --gecos "" myuser && \](#__codelineno-12-7)[chown -R myuser:myuser /app](#__codelineno-12-8)[COPY . .](#__codelineno-12-10)[USER myuser](#__codelineno-12-12)[ENV PATH="/home/myuser/.local/bin:$PATH"](#__codelineno-12-14)[CMD ["sh", "-c", "uvicorn main:app --host 0.0.0.0 --port $PORT"]](#__codelineno-12-16)

#### Defining Multiple Agents[¶](#defining-multiple-agents)

You can define and deploy multiple agents within the same Cloud Run instance by creating separate folders in the root of `your-project-directory/`

. Each folder represents one agent and must define a `root_agent`

in its configuration.

Example structure:

your-project-directory/
├── capital_agent/
│ ├── __init__.py
│ └── agent.py # contains `root_agent` definition
├── population_agent/
│ ├── __init__.py
│ └── agent.py # contains `root_agent` definition
└── ...


#### Deploy using `gcloud`

[¶](#deploy-using-gcloud)

Navigate to `your-project-directory`

in your terminal.

gcloud run deploy capital-agent-service \
--source . \
--region $GOOGLE_CLOUD_LOCATION \
--project $GOOGLE_CLOUD_PROJECT \
--allow-unauthenticated \
--set-env-vars="GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_LOCATION=$GOOGLE_CLOUD_LOCATION,GOOGLE_GENAI_USE_VERTEXAI=$GOOGLE_GENAI_USE_VERTEXAI"
# Add any other necessary environment variables your agent might need


`capital-agent-service`

: The name you want to give your Cloud Run service.`--source .`

: Tells gcloud to build the container image from the Dockerfile in the current directory.`--region`

: Specifies the deployment region.`--project`

: Specifies the GCP project.`--allow-unauthenticated`

: Allows public access to the service. Remove this flag for private services.`--set-env-vars`

: Passes necessary environment variables to the running container. Ensure you include all variables required by ADK and your agent (like API keys if not using Application Default Credentials).

`gcloud`

will build the Docker image, push it to Google Artifact Registry, and deploy it to Cloud Run. Upon completion, it will output the URL of your deployed service.

For a full list of deployment options, see the [ gcloud run deploy reference documentation](https://cloud.google.com/sdk/gcloud/reference/run/deploy).

### adk CLI[¶](#adk-cli_1)

The adkgo command is located in the google/adk-go repository under cmd/adkgo. Before using it, you need to build it from the root of the adk-go repository:

`go build ./cmd/adkgo`


The adkgo deploy cloudrun command automates the deployment of your application. You do not need to provide your own Dockerfile.

#### Agent Code Structure[¶](#agent-code-structure)

When using the adkgo tool, your main.go file must use the launcher framework. This is because the tool compiles your code and then runs the resulting executable with specific command-line arguments (like web, api, a2a) to start the required services. The launcher is designed to parse these arguments correctly.

Your main.go should look like this:

// Copyright 2025 Google LLC
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
// http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
package main
import (
"context"
"fmt"
"log"
"os"
"strings"
"google.golang.org/adk/agent"
"google.golang.org/adk/agent/llmagent"
"google.golang.org/adk/cmd/launcher"
"google.golang.org/adk/cmd/launcher/full"
"google.golang.org/adk/model/gemini"
"google.golang.org/adk/tool"
"google.golang.org/adk/tool/functiontool"
"google.golang.org/genai"
)
type getCapitalCityArgs struct {
Country string `json:"country" jsonschema:"The country for which to find the capital city."`
}
func getCapitalCity(ctx tool.Context, args getCapitalCityArgs) (string, error) {
capitals := map[string]string{
"united states": "Washington, D.C.",
"canada": "Ottawa",
"france": "Paris",
"japan": "Tokyo",
}
capital, ok := capitals[strings.ToLower(args.Country)]
if !ok {
return "", fmt.Errorf("couldn't find the capital for %s", args.Country)
}
return capital, nil
}
func main() {
ctx := context.Background()
model, err := gemini.NewModel(ctx, "gemini-2.5-flash", &genai.ClientConfig{
APIKey: os.Getenv("GOOGLE_API_KEY"),
})
if err != nil {
log.Fatalf("Failed to create model: %v", err)
}
capitalTool, err := functiontool.New(
functiontool.Config{
Name: "get_capital_city",
Description: "Retrieves the capital city for a given country.",
},
getCapitalCity,
)
if err != nil {
log.Fatalf("Failed to create function tool: %v", err)
}
geoAgent, err := llmagent.New(llmagent.Config{
Name: "capital_agent",
Model: model,
Description: "Agent to find the capital city of a country.",
Instruction: "I can answer your questions about the capital city of a country.",
Tools: []tool.Tool{capitalTool},
})
if err != nil {
log.Fatalf("Failed to create agent: %v", err)
}
config := &launcher.Config{
AgentLoader: agent.NewSingleLoader(geoAgent),
}
l := full.NewLauncher()
err = l.Execute(ctx, config, os.Args[1:])
if err != nil {
log.Fatalf("run failed: %v\n\n%s", err, l.CommandLineSyntax())
}
}


#### How it Works[¶](#how-it-works)

- The adkgo tool compiles your main.go into a statically linked binary for Linux.
- It generates a Dockerfile that copies this binary into a minimal container.
- It uses gcloud to build and deploy this container to Cloud Run.
- After deployment, it starts a local proxy that securely connects to your new service.

Ensure you have authenticated with Google Cloud (`gcloud auth login`

and `gcloud config set project <your-project-id>`

).

#### Setup environment variables[¶](#setup-environment-variables_1)

Optional but recommended: Setting environment variables can make the deployment commands cleaner.

# Set your Google Cloud Project ID
export GOOGLE_CLOUD_PROJECT="your-gcp-project-id"
# Set your desired Google Cloud Location
export GOOGLE_CLOUD_LOCATION="us-central1"
# Set the path to your agent's main Go file
export AGENT_PATH="./examples/go/cloud-run/main.go"
# Set a name for your Cloud Run service
export SERVICE_NAME="capital-agent-service"


#### Command usage[¶](#command-usage_1)

./adkgo deploy cloudrun \
-p $GOOGLE_CLOUD_PROJECT \
-r $GOOGLE_CLOUD_LOCATION \
-s $SERVICE_NAME \
--proxy_port=8081 \
--server_port=8080 \
-e $AGENT_PATH \
--a2a --api --webui


##### Required[¶](#required)

`-p, --project_name`

: Your Google Cloud project ID (e.g., $GOOGLE_CLOUD_PROJECT).`-r, --region`

: The Google Cloud location for deployment (e.g., $GOOGLE_CLOUD_LOCATION, us-central1).`-s, --service_name`

: The name for the Cloud Run service (e.g., $SERVICE_NAME).`-e, --entry_point_path`

: Path to the main Go file containing your agent's source code (e.g., $AGENT_PATH).

##### Optional[¶](#optional)

`--proxy_port`

: The local port for the authenticating proxy to listen on. Defaults to 8081.`--server_port`

: The port number the server will listen on within the Cloud Run container. Defaults to 8080.`--a2a`

: If included, enables Agent2Agent communication. Enabled by default.`--a2a_agent_url`

: A2A agent card URL as advertised in the public agent card. This flag is only valid when used with the --a2a flag.`--api`

: If included, deploys the ADK API server. Enabled by default.`--webui`

: If included, deploys the ADK dev UI alongside the agent API server. Enabled by default.`--temp_dir`

: Temp directory for build artifacts. Defaults to os.TempDir().`--help`

: Show the help message and exit.

##### Authenticated access[¶](#authenticated-access_1)

The service is deployed with --no-allow-unauthenticated by default.

Upon successful execution, the command deploys your agent to Cloud Run and provide a local URL to access the service through the proxy.

### gcloud CLI for Java[¶](#gcloud-cli-for-java)

You can deploy Java Agents using the standard `gcloud run deploy`

command and a `Dockerfile`

. This is the current recommended way to deploy Java Agents to Google Cloud Run.

Ensure you are [authenticated](https://cloud.google.com/docs/authentication/gcloud) with Google Cloud.
Specifically, run the commands `gcloud auth login`

and `gcloud config set project <your-project-id>`

from your terminal.

#### Project Structure[¶](#project-structure_1)

Organize your project files as follows:

your-project-directory/
├── src/
│ └── main/
│ └── java/
│ └── agents/
│ ├── capitalagent/
│ └── CapitalAgent.java # Your agent code
├── pom.xml # Java adk and adk-dev dependencies
└── Dockerfile # Container build instructions


Create the `pom.xml`

and `Dockerfile`

in the root of your project directory. Your Agent code file (`CapitalAgent.java`

) inside a directory as shown above.

#### Code files[¶](#code-files_1)

-
This is our Agent definition. This is the same code as present in

[LLM agent](../../agents/llm-agents/)with two caveats:-
The Agent is now initialized as a

**global public static final variable**. -
The definition of the agent can be exposed in a static method or inlined during declaration.


See the code for the

`CapitalAgent`

example in the[examples](https://github.com/google/adk-docs/blob/main/examples/java/cloud-run/src/main/java/agents/capitalagent/CapitalAgent.java)repository. -
-
Add the following dependencies and plugin to the pom.xml file.

pom.xml[<dependencies>](#__codelineno-19-1)[<dependency>](#__codelineno-19-2)[<groupId>com.google.adk</groupId>](#__codelineno-19-3)[<artifactId>google-adk</artifactId>](#__codelineno-19-4)[<version>0.5.0</version>](#__codelineno-19-5)[</dependency>](#__codelineno-19-6)[<dependency>](#__codelineno-19-7)[<groupId>com.google.adk</groupId>](#__codelineno-19-8)[<artifactId>google-adk-dev</artifactId>](#__codelineno-19-9)[<version>0.5.0</version>](#__codelineno-19-10)[</dependency>](#__codelineno-19-11)[</dependencies>](#__codelineno-19-12)[<plugin>](#__codelineno-19-14)[<groupId>org.codehaus.mojo</groupId>](#__codelineno-19-15)[<artifactId>exec-maven-plugin</artifactId>](#__codelineno-19-16)[<version>3.2.0</version>](#__codelineno-19-17)[<configuration>](#__codelineno-19-18)[<mainClass>com.google.adk.web.AdkWebServer</mainClass>](#__codelineno-19-19)[<classpathScope>compile</classpathScope>](#__codelineno-19-20)[</configuration>](#__codelineno-19-21)[</plugin>](#__codelineno-19-22) -
Define the container image:

Dockerfile[# Use an official Maven image with a JDK. Choose a version appropriate for your project.](#__codelineno-20-1)[FROM maven:3.8-openjdk-17 AS builder](#__codelineno-20-2)[WORKDIR /app](#__codelineno-20-4)[COPY pom.xml .](#__codelineno-20-6)[RUN mvn dependency:go-offline -B](#__codelineno-20-7)[COPY src ./src](#__codelineno-20-9)[# Expose the port your application will listen on.](#__codelineno-20-11)[# Cloud Run will set the PORT environment variable, which your app should use.](#__codelineno-20-12)[EXPOSE 8080](#__codelineno-20-13)[# The command to run your application.](#__codelineno-20-15)[# Use a shell so ${PORT} expands and quote exec.args so agent source-dir is passed correctly.](#__codelineno-20-16)[ENTRYPOINT ["sh", "-c", "mvn compile exec:java \](#__codelineno-20-17)[-Dexec.mainClass=com.google.adk.web.AdkWebServer \](#__codelineno-20-18)[-Dexec.classpathScope=compile \](#__codelineno-20-19)[-Dexec.args='--server.port=${PORT:-8080} --adk.agents.source-dir=target'"]](#__codelineno-20-20)

#### Deploy using `gcloud`

[¶](#deploy-using-gcloud_1)

Navigate to `your-project-directory`

in your terminal.

gcloud run deploy capital-agent-service \
--source . \
--region $GOOGLE_CLOUD_LOCATION \
--project $GOOGLE_CLOUD_PROJECT \
--allow-unauthenticated \
--set-env-vars="GOOGLE_CLOUD_PROJECT=$GOOGLE_CLOUD_PROJECT,GOOGLE_CLOUD_LOCATION=$GOOGLE_CLOUD_LOCATION,GOOGLE_GENAI_USE_VERTEXAI=$GOOGLE_GENAI_USE_VERTEXAI"
# Add any other necessary environment variables your agent might need


`capital-agent-service`

: The name you want to give your Cloud Run service.`--source .`

: Tells gcloud to build the container image from the Dockerfile in the current directory.`--region`

: Specifies the deployment region.`--project`

: Specifies the GCP project.`--allow-unauthenticated`

: Allows public access to the service. Remove this flag for private services.`--set-env-vars`

: Passes necessary environment variables to the running container. Ensure you include all variables required by ADK and your agent (like API keys if not using Application Default Credentials).

`gcloud`

will build the Docker image, push it to Google Artifact Registry, and deploy it to Cloud Run. Upon completion, it will output the URL of your deployed service.

For a full list of deployment options, see the [ gcloud run deploy reference documentation](https://cloud.google.com/sdk/gcloud/reference/run/deploy).

## Testing your agent[¶](#testing-your-agent)

Once your agent is deployed to Cloud Run, you can interact with it via the deployed UI (if enabled) or directly with its API endpoints using tools like `curl`

. You'll need the service URL provided after deployment.

### UI Testing[¶](#ui-testing)

If you deployed your agent with the UI enabled:

**adk CLI:**You included the`--webui`

flag during deployment.**gcloud CLI:**You set`SERVE_WEB_INTERFACE = True`

in your`main.py`

.

You can test your agent by simply navigating to the Cloud Run service URL provided after deployment in your web browser.

The ADK dev UI allows you to interact with your agent, manage sessions, and view execution details directly in the browser.

To verify your agent is working as intended, you can:

- Select your agent from the dropdown menu.
- Type a message and verify that you receive an expected response from your agent.

If you experience any unexpected behavior, check the [Cloud Run](https://console.cloud.google.com/run) console logs.

### API Testing (curl)[¶](#api-testing-curl)

You can interact with the agent's API endpoints using tools like `curl`

. This is useful for programmatic interaction or if you deployed without the UI.

You'll need the service URL provided after deployment and potentially an identity token for authentication if your service isn't set to allow unauthenticated access.

#### Set the application URL[¶](#set-the-application-url)

Replace the example URL with the actual URL of your deployed Cloud Run service.

export APP_URL="YOUR_CLOUD_RUN_SERVICE_URL"
# Example: export APP_URL="https://adk-default-service-name-abc123xyz.a.run.app"


#### Get an identity token (if needed)[¶](#get-an-identity-token-if-needed)

If your service requires authentication (i.e., you didn't use `--allow-unauthenticated`

with `gcloud`

or answered 'N' to the prompt with `adk`

), obtain an identity token.

*If your service allows unauthenticated access, you can omit the -H "Authorization: Bearer $TOKEN" header from the curl commands below.*


#### List available apps[¶](#list-available-apps)

Verify the deployed application name.

*(Adjust the app_name in the following commands based on this output if needed. The default is often the agent directory name, e.g., capital_agent)*.


#### Create or Update a Session[¶](#create-or-update-a-session)

Initialize or update the state for a specific user and session. Replace `capital_agent`

with your actual app name if different. The values `user_123`

and `session_abc`

are example identifiers; you can replace them with your desired user and session IDs.

curl -X POST -H "Authorization: Bearer $TOKEN" \
$APP_URL/apps/capital_agent/users/user_123/sessions/session_abc \
-H "Content-Type: application/json" \
-d '{"preferred_language": "English", "visit_count": 5}'


#### Run the Agent[¶](#run-the-agent)

Send a prompt to your agent. Replace `capital_agent`

with your app name and adjust the user/session IDs and prompt as needed.

curl -X POST -H "Authorization: Bearer $TOKEN" \
$APP_URL/run_sse \
-H "Content-Type: application/json" \
-d '{
"app_name": "capital_agent",
"user_id": "user_123",
"session_id": "session_abc",
"new_message": {
"role": "user",
"parts": [{
"text": "What is the capital of Canada?"
}]
},
"streaming": false
}'


- Set
`"streaming": true`

if you want to receive Server-Sent Events (SSE). - The response will contain the agent's execution events, including the final answer.

---
<!-- Source: N/A -->

---
<!-- Source: https://google.github.io/adk-docs/deploy/agent-engine/ -->

# Deploy to Vertex AI Agent Engine¶

# Deploy to Vertex AI Agent Engine[¶](#deploy-to-vertex-ai-agent-engine)

Google Cloud Vertex AI
[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
is a set of modular services that help developers scale and govern agents in
production. The Agent Engine runtime enables you to deploy agents in production
with end-to-end managed infrastructure so you can focus on creating intelligent
and impactful agents. When you deploy an ADK agent to Agent Engine, your code
runs in the *Agent Engine runtime* environment, which is part of the larger set
of agent services provided by the Agent Engine product.

This guide includes the following deployment paths, which serve different purposes:

-
: Follow this standard deployment path if you have an existing Google Cloud project and if you want to carefully manage deploying an ADK agent to the Agent Engine runtime. This deployment path uses Cloud Console, ADK command line interface, and provides step-by-step instructions. This path is recommended for users who are already familiar with configuring Google Cloud projects, and users preparing for production deployments.[Standard deployment](/adk-docs/deploy/agent-engine/deploy/) -
: Follow this accelerated deployment path if you do not have an existing Google Cloud project and are creating a project specifically for development and testing. The Agent Starter Pack (ASP) helps you deploy ADK projects quickly and it configures Google Cloud services that are not strictly necessary for running an ADK agent with the Agent Engine runtime.[Agent Starter Pack deployment](/adk-docs/deploy/agent-engine/asp/)

Agent Engine service on Google Cloud

Agent Engine is a paid service and you may incur costs if you go
above the no-cost access tier. More information can be found on the
[Agent Engine pricing page](https://cloud.google.com/vertex-ai/pricing#vertex-ai-agent-engine).

## Deployment payload[¶](#payload)

When you deploy your ADK agent project to Agent Engine, the following content is uploaded to the service:

- Your ADK agent code
- Any dependencies declared in your ADK agent code

The deployment *does not* include the ADK API server or the ADK web user
interface libraries. The Agent Engine service provides the libraries for ADK API
server functionality.

---
<!-- Source: https://google.github.io/adk-docs/deploy/agent-engine/asp/ -->

# Deploy to Agent Engine with Agent Starter Pack¶

# Deploy to Agent Engine with Agent Starter Pack[¶](#deploy-to-agent-engine-with-agent-starter-pack)

This deployment procedure describes how to perform a deployment using the
[Agent Starter Pack](https://github.com/GoogleCloudPlatform/agent-starter-pack)
(ASP) and the ADK command line interface (CLI) tool. Using ASP for deployment to
the Agent Engine runtime is an accelerated path, and you should use it for
* development and testing* only. The ASP tool configures Google Cloud resources
that are not strictly necessary for running an ADK agent workflow, and you
should thoroughly review that configuration before using it in a production
deployment.

This deployment guide uses the ASP tool to apply a project template to your existing project, add deployment artifacts, and prepare your agent project for deployment. These instructions show you how to use ASP to provision a Google Cloud project with services needed for deploying your ADK project, as follows:

[Prerequisites](#prerequisites-ad): Setup Google Cloud account, a project, and install required software.[Prepare your ADK project](#prepare-ad): Modify your existing ADK project files to get ready for deployment.[Connect to your Google Cloud project](#connect-ad): Connect your development environment to Google Cloud and your Google Cloud project.[Deploy your ADK project](#deploy-ad): Provision required services in your Google Cloud project and upload your ADK project code.

For information on testing a deployed agent, see [Test deployed agent](../test/).
For more information on using Agent Starter Pack and its command line tools,
see the
[CLI reference](https://googlecloudplatform.github.io/agent-starter-pack/cli/enhance.html)
and
[Development guide](https://googlecloudplatform.github.io/agent-starter-pack/guide/development-guide.html).

### Prerequisites[¶](#prerequisites-ad)

You need the following resources configured to use this deployment path:

**Google Cloud account**: with administrator access to the following:**Google Cloud Project**: An empty Google Cloud project with[billing enabled](https://cloud.google.com/billing/docs/how-to/modify-project). For information on creating projects, see[Creating and managing projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects).

**Python Environment**: A Python version supported by the[ASP project](https://googlecloudplatform.github.io/agent-starter-pack/guide/getting-started.html).**uv Tool:**Manage Python development environment and running ASP tools. For installation details, see[Install uv](https://docs.astral.sh/uv/getting-started/installation/).**Google Cloud CLI tool**: The gcloud command line interface. For installation details, see[Google Cloud Command Line Interface](https://cloud.google.com/sdk/docs/install).**Make tool**: Build automation tool. This tool is part of most Unix-based systems, for installation details, see the[Make tool](https://www.gnu.org/software/make/)documentation.

### Prepare your ADK project[¶](#prepare-ad)

When you deploy an ADK project to Agent Engine, you need some additional files to support the deployment operation. The following ASP command backs up your project and then adds files to your project for deployment purposes.

These instructions assume you have an existing ADK project that you are modifying
for deployment. If you do not have an ADK project, or want to use a test
project, complete the Python
[Quickstart](/adk-docs/get-started/quickstart/) guide,
which creates a
[multi_tool_agent](https://github.com/google/adk-docs/tree/main/examples/python/snippets/get-started/multi_tool_agent)
project. The following instructions use the `multi_tool_agent`

project as an
example.

To prepare your ADK project for deployment to Agent Engine:

-
In a terminal window of your development environment, navigate to the

**parent directory**that contains your agent folder. For example, if your project structure is:Navigate to

`your-project-directory/`

-
Run the ASP

`enhance`

command to add the files required for deployment into your project. -
Follow the instructions from the ASP tool. In general, you can accept the default answers to all questions. However for the

**GCP region**, option, make sure you select one of the[supported regions](https://docs.cloud.google.com/agent-builder/locations#supported-regions-agent-engine)for Agent Engine.

When you successfully complete this process, the tool shows the following message:

Note

The ASP tool may show a reminder to connect to Google Cloud while
running, but that connection is *not required* at this stage.

For more information about the changes ASP makes to your ADK project, see
[Changes to your ADK project](#adk-asp-changes).

### Connect to your Google Cloud project[¶](#connect-ad)

Before you deploy your ADK project, you must connect to Google Cloud and your project. After logging into your Google Cloud account, you should verify that your deployment target project is visible from your account and that it is configured as your current project.

To connect to Google Cloud and list your project:

-
In a terminal window of your development environment, login to your Google Cloud account:

-
Set your target project using the Google Cloud Project ID:

-
Verify your Google Cloud target project is set:


Once you have successfully connected to Google Cloud and set your Cloud Project ID, you are ready to deploy your ADK project files to Agent Engine.

### Deploy your ADK project[¶](#deploy-ad)

When using the ASP tool, you deploy in stages. In the first stage, you run a
`make`

command that provisions the services needed to run your ADK workflow on
Agent Engine. In the second stage, the tool uploads your project code to the
Agent Engine service and runs it in the hosted environment

Important

*Make sure your Google Cloud target deployment project is set as your ***current
project*** before performing these steps*. The `make backend`

command uses
your currently set Google Cloud project when it performs a deployment. For
information on setting and checking your current project, see
[Connect to your Google Cloud project](#connect-ad).

To deploy your ADK project to Agent Engine in your Google Cloud project:

-
In a terminal window, ensure you are in the parent directory (e.g.,

`your-project-directory/`

) that contains your agent folder. -
Deploy the code from the updated local project into the Google Cloud development environment, by running the following ASP make command:


Once this process completes successfully, you should be able to interact with
the agent running on Google Cloud Agent Engine. For details on testing the
deployed agent, see
[Test deployed agent](/adk-docs/deploy/agent-engine/test/).

### Changes to your ADK project[¶](#adk-asp-changes)

The ASP tools add more files to your project for deployment. The procedure
below backs up your existing project files before modifying them. This guide
uses the
[multi_tool_agent](https://github.com/google/adk-docs/tree/main/examples/python/snippets/get-started/multi_tool_agent)
project as a reference example. The original project has the following file
structure to start with:

After running the ASP enhance command to add Agent Engine deployment information, the new structure is as follows:

multi-tool-agent/
├─ app/ # Core application code
│ ├─ agent.py # Main agent logic
│ ├─ agent_engine_app.py # Agent Engine application logic
│ └─ utils/ # Utility functions and helpers
├─ .cloudbuild/ # CI/CD pipeline configurations for Google Cloud Build
├─ deployment/ # Infrastructure and deployment scripts
├─ notebooks/ # Jupyter notebooks for prototyping and evaluation
├─ tests/ # Unit, integration, and load tests
├─ Makefile # Makefile for common commands
├─ GEMINI.md # AI-assisted development guide
└─ pyproject.toml # Project dependencies and configuration


See the *README.md* file in your updated ADK project folder for more information.
For more information on using Agent Starter Pack, see the
[Development guide](https://googlecloudplatform.github.io/agent-starter-pack/guide/development-guide.html).

## Test deployed agents[¶](#test-deployed-agents)

After completing deployment of your ADK agent you should test the workflow in
its new hosted environment. For more information on testing an ADK agent
deployed to Agent Engine, see
[Test deployed agents in Agent Engine](/adk-docs/deploy/agent-engine/test/).

---
<!-- Source: https://google.github.io/adk-docs/deploy/agent-engine/deploy/ -->

# Deploy to Vertex AI Agent Engine¶

# Deploy to Vertex AI Agent Engine[¶](#deploy-to-vertex-ai-agent-engine)

This deployment procedure describes how to perform a standard deployment of
ADK agent code to Google Cloud
[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview).
You should follow this deployment path if you have an existing Google Cloud
project and if you want to carefully manage deploying an ADK agent to Agent
Engine runtime environment. These instructions use Cloud Console, the gcloud
command line interface, and the ADK command line interface (ADK CLI). This path
is recommended for users who are already familiar with configuring Google Cloud
projects, and users preparing for production deployments.

These instructions describe how to deploy an ADK project to Google Cloud Agent Engine runtime environment, which includes the following stages:

## Setup Google Cloud project[¶](#setup-cloud-project)

To deploy your agent to Agent Engine, you need a Google Cloud project:

-
**Sign into Google Cloud**:- If you're an
**existing user**of Google Cloud:- Sign in via
[https://console.cloud.google.com](https://console.cloud.google.com) - If you previously used a Free Trial that has expired, you may need to
upgrade to a
[Paid billing account](https://docs.cloud.google.com/free/docs/free-cloud-features#how-to-upgrade).

- Sign in via
- If you are a
**new user**of Google Cloud:- You can sign up for the
[Free Trial program](https://docs.cloud.google.com/free/docs/free-cloud-features). The Free Trial gets you a $300 Welcome credit to spend over 91 days on various[Google Cloud products](https://docs.cloud.google.com/free/docs/free-cloud-features#during-free-trial)and you won't be billed. During the Free Trial, you also get access to the[Google Cloud Free Tier](https://docs.cloud.google.com/free/docs/free-cloud-features#free-tier), which gives you free usage of select products up to specified monthly limits, and to product-specific free trials.

- You can sign up for the

- If you're an
-
**Create a Google Cloud project**- If you already have an existing Google Cloud project, you can use it, but be aware this process is likely to add new services to the project.
- If you want to create a new Google Cloud project, you can create a new one
on the
[Create Project](https://console.cloud.google.com/projectcreate)page.

-
**Get your Google Cloud Project ID**- You need your Google Cloud Project ID, which you can find on your GCP
homepage. Make sure to note the Project ID (alphanumeric with hyphens),
*not*the project number (numeric).

- You need your Google Cloud Project ID, which you can find on your GCP
homepage. Make sure to note the Project ID (alphanumeric with hyphens),
-
**Enable Vertex AI in your project**- To use Agent Engine, you need to
[enable the Vertex AI API](https://console.cloud.google.com/apis/library/aiplatform.googleapis.com). Click on the "Enable" button to enable the API. Once enabled, it should say "API Enabled".

- To use Agent Engine, you need to
-
**Enable Cloud Resource Manager API in your project**- To use Agent Engine, you need to
[enable the Cloud Resource Manager API](https://console.developers.google.com/apis/api/cloudresourcemanager.googleapis.com/overview). Click on the "Enable" button to enable the API. Once enabled, it should say "API Enabled".

- To use Agent Engine, you need to

## Set up your coding environment[¶](#prerequisites-coding-env)

Now that you prepared your Google Cloud project, you can return to your coding environment. These steps require access to a terminal within your coding environment to run command line instructions.

### Authenticate your coding environment with Google Cloud[¶](#authenticate-your-coding-environment-with-google-cloud)

-
You need to authenticate your coding environment so that you and your code can interact with Google Cloud. To do so, you need the gcloud CLI. If you have never used the gcloud CLI, you need to first

[download and install it](https://docs.cloud.google.com/sdk/docs/install-sdk)before continuing with the steps below: -
Run the following command in your terminal to access your Google Cloud project as a user:

After authenticating, you should see the message

`You are now authenticated with the gcloud CLI!`

. -
Run the following command to authenticate your code so that it can work with Google Cloud:

After authenticating, you should see the message

`You are now authenticated with the gcloud CLI!`

. -
(Optional) If you need to set or change your default project in gcloud, you can use:


### Define your agent[¶](#define-your-agent)

With your Google Cloud and coding environment prepared, you're ready to deploy your agent. The instructions assume that you have an agent project folder, such as:

For more details on the project files and format, see the
[multi_tool_agent](https://github.com/google/adk-docs/tree/main/examples/python/snippets/get-started/multi_tool_agent)
code sample.

## Deploy the agent[¶](#deploy-agent)

You can deploy from your terminal using the `adk deploy`

command line tool. This
process packages your code, builds it into a container, and deploys it to the
managed Agent Engine service. This process can take several minutes.

The following example deploy command uses the `multi_tool_agent`

sample code as
the project to be deployed:

PROJECT_ID=my-project-id
LOCATION_ID=us-central1
adk deploy agent_engine \
--project=$PROJECT_ID \
--region=$LOCATION_ID \
--display_name="My First Agent" \
multi_tool_agent


For `region`

, you can find a list of the supported regions on the
[Vertex AI Agent Builder locations page](https://docs.cloud.google.com/agent-builder/locations#supported-regions-agent-engine).
To learn about the CLI options for the `adk deploy agent_engine`

command, see the
[ADK CLI Reference](https://google.github.io/adk-docs/api-reference/cli/cli.html#adk-deploy-agent-engine).

### Deploy command output[¶](#deploy-command-output)

Once successfully deployed, you should see the following output:

Creating AgentEngine
Create AgentEngine backing LRO: projects/123456789/locations/us-central1/reasoningEngines/751619551677906944/operations/2356952072064073728
View progress and logs at https://console.cloud.google.com/logs/query?project=hopeful-sunset-478017-q0
AgentEngine created. Resource name: projects/123456789/locations/us-central1/reasoningEngines/751619551677906944
To use this AgentEngine in another session:
agent_engine = vertexai.agent_engines.get('projects/123456789/locations/us-central1/reasoningEngines/751619551677906944')
Cleaning up the temp folder: /var/folders/k5/pv70z5m92s30k0n7hfkxszfr00mz24/T/agent_engine_deploy_src/20251219_134245


Note that you now have a `RESOURCE_ID`

where your agent has been deployed (which
in the example above is `751619551677906944`

). You need this ID number along
with the other values to use your agent on Agent Engine.

## Using an agent on Agent Engine[¶](#using-an-agent-on-agent-engine)

Once you have completed deployment of your ADK project, you can query the agent using the Vertex AI SDK, Python requests library, or a REST API client. This section provides some information on what you need to interact with your agent and how to construct URLs to interact with your agent's REST API.

To interact with your agent on Agent Engine, you need the following:

**PROJECT_ID**(example: "my-project-id") which you can find on your[project details page](https://console.cloud.google.com/iam-admin/settings)**LOCATION_ID**(example: "us-central1"), that you used to deploy your agent**RESOURCE_ID**(example: "751619551677906944"), which you can find on the[Agent Engine UI](https://console.cloud.google.com/vertex-ai/agents/agent-engines)

The query URL structure is as follows:

https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query


You can make requests from your agent using this URL structure. For more information
on how to make requests, see the instructions in the Agent Engine documentation
[Use an Agent Development Kit agent](https://docs.cloud.google.com/agent-builder/agent-engine/use/adk#rest-api).
You can also check the Agent Engine documentation to learn about how to manage your
[deployed agent](https://docs.cloud.google.com/agent-builder/agent-engine/manage/overview).
For more information on testing and interacting with a deployed agent, see
[Test deployed agents in Agent Engine](/adk-docs/deploy/agent-engine/test/).

### Monitoring and verification[¶](#monitoring-and-verification)

- You can monitor the deployment status in the
[Agent Engine UI](https://console.cloud.google.com/vertex-ai/agents/agent-engines)in the Google Cloud Console. - For additional details, you can visit the Agent Engine documentation
[deploying an agent](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/deploy)and[managing deployed agents](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/manage/overview).

## Test deployed agents[¶](#test-deployed-agents)

After completing deployment of your ADK agent you should test the workflow in
its new hosted environment. For more information on testing an ADK agent
deployed to Agent Engine, see
[Test deployed agents in Agent Engine](/adk-docs/deploy/agent-engine/test/).

---
<!-- Source: https://google.github.io/adk-docs/deploy/agent-engine/test/ -->

# Test deployed agents in Agent Engine¶

# Test deployed agents in Agent Engine[¶](#test-deployed-agents-in-agent-engine)

These instructions explain how to test an ADK agent deployed to the
[Agent Engine](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/overview)
runtime environment. Before using these instructions, you need to have completed
the deployment of your agent to the Agent Engine runtime environment using one
of the [available methods](/adk-docs/deploy/agent-engine/). This guide shows you
how to view, interact, and test your deployed agent through the Google Cloud
Console, and interact with the agent using REST API calls or the Vertex AI SDK
for Python.

## View deployed agent in Cloud Console[¶](#view-deployed-agent-in-cloud-console)

To view your deployed agent in the Cloud Console:

- Navigate to the Agent Engine page in the Google Cloud Console:
[https://console.cloud.google.com/vertex-ai/agents/agent-engines](https://console.cloud.google.com/vertex-ai/agents/agent-engines)

This page lists all deployed agents in your currently selected Google Cloud
project. If you do not see your agent listed, make sure you have your
target project selected in Google Cloud Console. For more information on
selecting an existing Google Cloud project, see
[Creating and managing projects](https://cloud.google.com/resource-manager/docs/creating-managing-projects#identifying_projects).

## Find Google Cloud project information[¶](#find-google-cloud-project-information)

You need the address and resource identification for your project (`PROJECT_ID`

,
`LOCATION_ID`

, `RESOURCE_ID`

) to be able to test your deployment. You can use Cloud
Console or the `gcloud`

command line tool to find this information.

## Vertex AI express mode API key

If you are using Vertex AI express mode, you can skip this step and use your API key.

To find your project information with Google Cloud Console:

-
In the Google Cloud Console, navigate to the Agent Engine page:

[https://console.cloud.google.com/vertex-ai/agents/agent-engines](https://console.cloud.google.com/vertex-ai/agents/agent-engines) -
At the top of the page, select

**API URLs**, and then copy the**Query URL**string for your deployed agent, which should be in this format:`https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query`


To find your project information with the `gcloud`

command line tool:

-
In your development environment, make sure you are authenticated to Google Cloud and run the following command to list your project:

-
With the Project ID you used for deployment, run this command to get the additional details:


## Test using REST calls[¶](#test-using-rest-calls)

A simple way to interact with your deployed agent in Agent Engine is to use REST
calls with the `curl`

tool. This section describes how to check your
connection to the agent and also to test processing of a request by the deployed
agent.

### Check connection to agent[¶](#check-connection-to-agent)

You can check your connection to the running agent using the **Query URL**
available in the Agent Engine section of the Cloud Console. This check does not
execute the deployed agent, but returns information about the agent.

To send a REST call and get a response from deployed agent:

-
In a terminal window of your development environment, build a request and execute it:


If your deployment was successful, this request responds with a list of valid requests and expected data formats.

Remove `:query`

parameter for connection URL

If you use the **Query URL** available in the Agent Engine section of the Cloud
Console, make sure to remove the `:query`

parameter from end of the address.

Access for agent connections

This connection test requires the calling user has a valid access token for the deployed agent. When testing from other environments, make sure the calling user has access to connect to the agent in your Google Cloud project.

### Send an agent request[¶](#send-an-agent-request)

When getting responses from your agent project, you must first create a session, receive a Session ID, and then send your requests using that Session ID. This process is described in the following instructions.

To test interaction with the deployed agent via REST:

-
In a terminal window of your development environment, create a session by building a request using this template:

[curl \](#__codelineno-4-1)[-H "Authorization: Bearer $(gcloud auth print-access-token)" \](#__codelineno-4-2)[-H "Content-Type: application/json" \](#__codelineno-4-3)[https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query \](#__codelineno-4-4)[-d '{"class_method": "async_create_session", "input": {"user_id": "u_123"},}'](#__codelineno-4-5) -
In the response from the previous command, extract the created

**Session ID**from the**id**field: -
In a terminal window of your development environment, send a message to your agent by building a request using this template and the Session ID created in the previous step:

[curl \](#__codelineno-7-1)[-H "Authorization: Bearer $(gcloud auth print-access-token)" \](#__codelineno-7-2)[-H "Content-Type: application/json" \](#__codelineno-7-3)[https://$(LOCATION_ID)-aiplatform.googleapis.com/v1/projects/$(PROJECT_ID)/locations/$(LOCATION_ID)/reasoningEngines/$(RESOURCE_ID):query?alt=sse -d '{](#__codelineno-7-4)["class_method": "async_stream_query",](#__codelineno-7-5)["input": {](#__codelineno-7-6)["user_id": "u_123",](#__codelineno-7-7)["session_id": "4857885913439920384",](#__codelineno-7-8)["message": "Hey whats the weather in new york today?",](#__codelineno-7-9)[}](#__codelineno-7-10)[}'](#__codelineno-7-11)[curl \](#__codelineno-8-1)[-H "x-goog-api-key:YOUR-EXPRESS-MODE-API-KEY" \](#__codelineno-8-2)[-H "Content-Type: application/json" \](#__codelineno-8-3)[https://aiplatform.googleapis.com/v1/reasoningEngines/$(RESOURCE_ID):query?alt=sse -d '{](#__codelineno-8-4)["class_method": "async_stream_query",](#__codelineno-8-5)["input": {](#__codelineno-8-6)["user_id": "u_123",](#__codelineno-8-7)["session_id": "4857885913439920384",](#__codelineno-8-8)["message": "Hey whats the weather in new york today?",](#__codelineno-8-9)[}](#__codelineno-8-10)[}'](#__codelineno-8-11)

This request should generate a response from your deployed agent code in JSON
format. For more information about interacting with a deployed ADK agent in
Agent Engine using REST calls, see
[Manage deployed agents](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/manage/overview#console)
and
[Use an Agent Development Kit agent](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/use/adk)
in the Agent Engine documentation.

## Test using Python[¶](#test-using-python)

You can use Python code for more sophisticated and repeatable testing of your agent deployed in Agent Engine. These instructions describe how to create a session with the deployed agent, and then send a request to the agent for processing.

### Create a remote session[¶](#create-a-remote-session)

Use the `remote_app`

object to create a connection to a deployed, remote agent:

# If you are in a new script or used the ADK CLI to deploy, you can connect like this:
# remote_app = agent_engines.get("your-agent-resource-name")
remote_session = await remote_app.async_create_session(user_id="u_456")
print(remote_session)


Expected output for `create_session`

(remote):

{'events': [],
'user_id': 'u_456',
'state': {},
'id': '7543472750996750336',
'app_name': '7917477678498709504',
'last_update_time': 1743683353.030133}


The `id`

value is the session ID, and `app_name`

is the resource ID of the
deployed agent on Agent Engine.

#### Send queries to your remote agent[¶](#send-queries-to-your-remote-agent)

async for event in remote_app.async_stream_query(
user_id="u_456",
session_id=remote_session["id"],
message="whats the weather in new york",
):
print(event)


Expected output for `async_stream_query`

(remote):

{'parts': [{'function_call': {'id': 'af-f1906423-a531-4ecf-a1ef-723b05e85321', 'args': {'city': 'new york'}, 'name': 'get_weather'}}], 'role': 'model'}
{'parts': [{'function_response': {'id': 'af-f1906423-a531-4ecf-a1ef-723b05e85321', 'name': 'get_weather', 'response': {'status': 'success', 'report': 'The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit).'}}}], 'role': 'user'}
{'parts': [{'text': 'The weather in New York is sunny with a temperature of 25 degrees Celsius (41 degrees Fahrenheit).'}], 'role': 'model'}


For more information about interacting with a deployed ADK agent in
Agent Engine, see
[Manage deployed agents](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/manage/overview)
and
[Use a Agent Development Kit agent](https://cloud.google.com/vertex-ai/generative-ai/docs/agent-engine/use/adk)
in the Agent Engine documentation.

### Sending Multimodal Queries[¶](#sending-multimodal-queries)

To send multimodal queries (e.g., including images) to your agent, you can construct the `message`

parameter of `async_stream_query`

with a list of `types.Part`

objects. Each part can be text or an image.

To include an image, you can use `types.Part.from_uri`

, providing a Google Cloud Storage (GCS) URI for the image.

from google.genai import types
image_part = types.Part.from_uri(
file_uri="gs://cloud-samples-data/generative-ai/image/scones.jpg",
mime_type="image/jpeg",
)
text_part = types.Part.from_text(
text="What is in this image?",
)
async for event in remote_app.async_stream_query(
user_id="u_456",
session_id=remote_session["id"],
message=[text_part, image_part],
):
print(event)


Note

While the underlying communication with the model may involve Base64 encoding for images, the recommended and supported method for sending image data to an agent deployed on Agent Engine is by providing a GCS URI.

## Clean up deployments[¶](#clean-up-deployments)

If you have performed deployments as tests, it is a good practice to clean up your cloud resources after you have finished. You can delete the deployed Agent Engine instance to avoid any unexpected charges on your Google Cloud account.

The `force=True`

parameter also deletes any child resources that were generated
from the deployed agent, such as sessions. You can also delete your deployed
agent via the
[Agent Engine UI](https://console.cloud.google.com/vertex-ai/agents/agent-engines)
on Google Cloud.
