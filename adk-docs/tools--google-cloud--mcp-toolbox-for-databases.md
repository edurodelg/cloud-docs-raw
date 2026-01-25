---
source_url: https://google.github.io/adk-docs/tools/google-cloud/mcp-toolbox-for-databases/
fetched_at: 2026-01-25T03:11:33.244355
---

# MCP Toolbox for Databases¶

# MCP Toolbox for Databases[¶](#mcp-toolbox-for-databases)

[MCP Toolbox for Databases](https://github.com/googleapis/genai-toolbox) is an
open source MCP server for databases. It was designed with enterprise-grade and
production-quality in mind. It enables you to develop tools easier, faster, and
more securely by handling the complexities such as connection pooling,
authentication, and more.

Google’s Agent Development Kit (ADK) has built in support for Toolbox. For more
information on
[getting started](https://googleapis.github.io/genai-toolbox/getting-started/) or
[configuring](https://googleapis.github.io/genai-toolbox/getting-started/configure/)
Toolbox, see the
[documentation](https://googleapis.github.io/genai-toolbox/getting-started/introduction/).

## Supported Data Sources[¶](#supported-data-sources)

MCP Toolbox provides out-of-the-box toolsets for the following databases and data platforms:

### Google Cloud[¶](#google-cloud)

[BigQuery](https://googleapis.github.io/genai-toolbox/resources/sources/bigquery/)(including tools for SQL execution, schema discovery, and AI-powered time series forecasting)[AlloyDB](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-pg/)(PostgreSQL-compatible, with tools for both standard queries and natural language queries)[AlloyDB Admin](https://googleapis.github.io/genai-toolbox/resources/sources/alloydb-admin/)[Spanner](https://googleapis.github.io/genai-toolbox/resources/sources/spanner/)(supporting both GoogleSQL and PostgreSQL dialects)- Cloud SQL (with dedicated support for
[Cloud SQL for PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-pg/),[Cloud SQL for MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mysql/), and[Cloud SQL for SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-mssql/)) [Cloud SQL Admin](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-sql-admin/)[Firestore](https://googleapis.github.io/genai-toolbox/resources/sources/firestore/)[Bigtable](https://googleapis.github.io/genai-toolbox/resources/sources/bigtable/)[Dataplex](https://googleapis.github.io/genai-toolbox/resources/sources/dataplex/)(for data discovery and metadata search)[Cloud Monitoring](https://googleapis.github.io/genai-toolbox/resources/sources/cloud-monitoring/)

### Relational & SQL Databases[¶](#relational-sql-databases)

[PostgreSQL](https://googleapis.github.io/genai-toolbox/resources/sources/postgres/)(generic)[MySQL](https://googleapis.github.io/genai-toolbox/resources/sources/mysql/)(generic)[Microsoft SQL Server](https://googleapis.github.io/genai-toolbox/resources/sources/mssql/)(generic)[ClickHouse](https://googleapis.github.io/genai-toolbox/resources/sources/clickhouse/)[TiDB](https://googleapis.github.io/genai-toolbox/resources/sources/tidb/)[OceanBase](https://googleapis.github.io/genai-toolbox/resources/sources/oceanbase/)[Firebird](https://googleapis.github.io/genai-toolbox/resources/sources/firebird/)[SQLite](https://googleapis.github.io/genai-toolbox/resources/sources/sqlite/)[YugabyteDB](https://googleapis.github.io/genai-toolbox/resources/sources/yugabytedb/)

### NoSQL & Key-Value Stores[¶](#nosql-key-value-stores)

### Graph Databases[¶](#graph-databases)

### Data Platforms & Federation[¶](#data-platforms-federation)

[Looker](https://googleapis.github.io/genai-toolbox/resources/sources/looker/)(for running Looks, queries, and building dashboards via the Looker API)[Trino](https://googleapis.github.io/genai-toolbox/resources/sources/trino/)(for running federated queries across multiple sources)

### Other[¶](#other)

## Configure and deploy[¶](#configure-and-deploy)

Toolbox is an open source server that you deploy and manage yourself. For more instructions on deploying and configuring, see the official Toolbox documentation:

## Install Client SDK for ADK[¶](#install-client-sdk-for-adk)

ADK relies on the `toolbox-adk`

python package to use Toolbox. Install the
package before getting started:

### Loading Toolbox Tools[¶](#loading-toolbox-tools)

Once your Toolbox server is configured, up and running, you can load tools from your server using ADK:

from google.adk.agents import Agent
from google.adk.tools.toolbox_toolset import ToolboxToolset
toolset = ToolboxToolset(
server_url="http://127.0.0.1:5000"
)
root_agent = Agent(
...,
tools=[toolset] # Provide the toolset to the Agent
)


### Authentication[¶](#authentication)

The `ToolboxToolset`

supports various authentication strategies including Workload Identity (ADC), User Identity (OAuth2), and API Keys. For full documentation, see the [Toolbox ADK Authentication Guide](https://github.com/googleapis/mcp-toolbox-sdk-python/tree/main/packages/toolbox-adk#authentication).

**Example: Workload Identity (ADC)**

Recommended for Cloud Run, GKE, or local development with `gcloud auth login`

.

from google.adk.tools.toolbox_toolset import ToolboxToolset
from toolbox_adk import CredentialStrategy
# target_audience: The URL of your Toolbox server
creds = CredentialStrategy.workload_identity(target_audience="<TOOLBOX_URL>")
toolset = ToolboxToolset(
server_url="<TOOLBOX_URL>",
credentials=creds
)


### Advanced Configuration[¶](#advanced-configuration)

You can configure parameter binding, request hooks, and additional headers. See the [Toolbox ADK documentation](https://github.com/googleapis/mcp-toolbox-sdk-python/tree/main/packages/toolbox-adk) for details.

#### Parameter Binding[¶](#parameter-binding)

Bind values to tool parameters globally. These values are hidden from the model.

toolset = ToolboxToolset(
server_url="...",
bound_params={
"region": "us-central1",
"api_key": lambda: get_api_key() # Can be a callable
}
)


#### Usage with Hooks[¶](#usage-with-hooks)

Attach `pre_hook`

and `post_hook`

functions to execute logic before and after tool invocation.

ADK relies on the `@toolbox-sdk/adk`

TS package to use Toolbox. Install the
package before getting started:

### Loading Toolbox Tools[¶](#loading-toolbox-tools_1)

Once you’re Toolbox server is configured and up and running, you can load tools from your server using ADK:

import {InMemoryRunner, LlmAgent} from '@google/adk';
import {Content} from '@google/genai';
import {ToolboxClient} from '@toolbox-sdk/adk'
const toolboxClient = new ToolboxClient("http://127.0.0.1:5000");
const loadedTools = await toolboxClient.loadToolset();
export const rootAgent = new LlmAgent({
name: 'weather_time_agent',
model: 'gemini-2.5-flash',
description:
'Agent to answer questions about the time and weather in a city.',
instruction:
'You are a helpful agent who can answer user questions about the time and weather in a city.',
tools: loadedTools,
});
async function main() {
const userId = 'test_user';
const appName = rootAgent.name;
const runner = new InMemoryRunner({agent: rootAgent, appName});
const session = await runner.sessionService.createSession({
appName,
userId,
});
const prompt = 'What is the weather in New York? And the time?';
const content: Content = {
role: 'user',
parts: [{text: prompt}],
};
console.log(content);
for await (const e of runner.runAsync({
userId,
sessionId: session.id,
newMessage: content,
})) {
if (e.content?.parts?.[0]?.text) {
console.log(`${e.author}: ${JSON.stringify(e.content, null, 2)}`);
}
}
}
main().catch(console.error);


ADK relies on the `mcp-toolbox-sdk-go`

go module to use Toolbox. Install the
module before getting started:

### Loading Toolbox Tools[¶](#loading-toolbox-tools_2)

Once you’re Toolbox server is configured and up and running, you can load tools from your server using ADK:

package main
import (
"context"
"fmt"
"github.com/googleapis/mcp-toolbox-sdk-go/tbadk"
"google.golang.org/adk/agent/llmagent"
)
func main() {
toolboxClient, err := tbadk.NewToolboxClient("https://127.0.0.1:5000")
if err != nil {
log.Fatalf("Failed to create MCP Toolbox client: %v", err)
}
// Load a specific set of tools
toolboxtools, err := toolboxClient.LoadToolset("my-toolset-name", ctx)
if err != nil {
return fmt.Sprintln("Could not load Toolbox Toolset", err)
}
toolsList := make([]tool.Tool, len(toolboxtools))
for i := range toolboxtools {
toolsList[i] = &toolboxtools[i]
}
llmagent, err := llmagent.New(llmagent.Config{
...,
Tools: toolsList,
})
// Load a single tool
tool, err := client.LoadTool("my-tool-name", ctx)
if err != nil {
return fmt.Sprintln("Could not load Toolbox Tool", err)
}
llmagent, err := llmagent.New(llmagent.Config{
...,
Tools: []tool.Tool{&toolboxtool},
})
}


## Advanced Toolbox Features[¶](#advanced-toolbox-features)

Toolbox has a variety of features to make developing Gen AI tools for databases. For more information, read more about the following features:

[Authenticated Parameters](https://googleapis.github.io/genai-toolbox/resources/tools/#authenticated-parameters): bind tool inputs to values from OIDC tokens automatically, making it easy to run sensitive queries without potentially leaking data[Authorized Invocations:](https://googleapis.github.io/genai-toolbox/resources/tools/#authorized-invocations)restrict access to use a tool based on the users Auth token[OpenTelemetry](https://googleapis.github.io/genai-toolbox/how-to/export_telemetry/): get metrics and tracing from Toolbox with OpenTelemetry