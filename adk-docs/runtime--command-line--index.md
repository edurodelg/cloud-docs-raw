---
source_url: https://google.github.io/adk-docs/runtime/command-line/
fetched_at: 2026-01-25T02:05:49.677863
---

# Use the Command Line¶

# Use the Command Line[¶](#use-the-command-line)

ADK provides an interactive terminal interface for testing your agents. This is useful for quick testing, scripted interactions, and CI/CD pipelines.

## Run an agent[¶](#run-an-agent)

Use the following command to run your agent in the ADK command line interface:

Create an `AgentCliRunner`

class (see [Java Quickstart](../../get-started/java/)) and run:

This starts an interactive session where you can type queries and see agent responses directly in your terminal:

Running agent my_agent, type exit to exit.
[user]: What's the weather in New York?
[my_agent]: The weather in New York is sunny with a temperature of 25°C.
[user]: exit


## Session options[¶](#session-options)

The `adk run`

command includes options for saving, resuming, and replaying
sessions.

### Save sessions[¶](#save-sessions)

To save the session when you exit:

You'll be prompted to enter a session ID, and the session will be saved to
`path/to/my_agent/<session_id>.session.json`

.

You can also specify the session ID upfront:

### Resume sessions[¶](#resume-sessions)

To continue a previously saved session:

This loads the previous session state and event history, displays it, and allows you to continue the conversation.

### Replay sessions[¶](#replay-sessions)

To replay a session file without interactive input:

The input file should contain initial state and queries:

## Storage options[¶](#storage-options)

| Option | Description | Default |
|---|---|---|
`--session_service_uri` |
Custom session storage URI | SQLite under `.adk/session.db` |
`--artifact_service_uri` |
Custom artifact storage URI | Local `.adk/artifacts` |

### Example with storage options[¶](#example-with-storage-options)

## All options[¶](#all-options)

| Option | Description |
|---|---|
`--save_session` |
Save the session to a JSON file on exit |
`--session_id` |
Session ID to use when saving |
`--resume` |
Path to a saved session file to resume |
`--replay` |
Path to an input file for non-interactive replay |
`--session_service_uri` |
Custom session storage URI |
`--artifact_service_uri` |
Custom artifact storage URI |