---
source_url: https://google.github.io/adk-docs/observability/logging/
fetched_at: 2026-01-25T03:12:53.405970
---

# Logging in the Agent Development Kit (ADK)¶

# Logging in the Agent Development Kit (ADK)[¶](#logging-in-the-agent-development-kit-adk)

The Agent Development Kit (ADK) uses Python's standard `logging`

module to provide flexible and powerful logging capabilities. Understanding how to configure and interpret these logs is crucial for monitoring agent behavior and debugging issues effectively.

## Logging Philosophy[¶](#logging-philosophy)

ADK's approach to logging is to provide detailed diagnostic information without being overly verbose by default. It is designed to be configured by the application developer, allowing you to tailor the log output to your specific needs, whether in a development or production environment.

**Standard Library:**It uses the standard`logging`

library, so any configuration or handler that works with it will work with ADK.**Hierarchical Loggers:**Loggers are named hierarchically based on the module path (e.g.,`google_adk.google.adk.agents.llm_agent`

), allowing for fine-grained control over which parts of the framework produce logs.**User-Configured:**The framework does not configure logging itself. It is the responsibility of the developer using the framework to set up the desired logging configuration in their application's entry point.

## How to Configure Logging[¶](#how-to-configure-logging)

You can configure logging in your main application script (e.g., `main.py`

) before you initialize and run your agent. The simplest way is to use `logging.basicConfig`

.

### Example Configuration[¶](#example-configuration)

To enable detailed logging, including `DEBUG`

level messages, add the following to the top of your script:

import logging
logging.basicConfig(
level=logging.DEBUG,
format='%(asctime)s - %(levelname)s - %(name)s - %(message)s'
)
# Your ADK agent code follows...
# from google.adk.agents import LlmAgent
# ...


### Configuring Logging with the ADK CLI[¶](#configuring-logging-with-the-adk-cli)

When running agents using the ADK's built-in web or API servers, you can easily control the log verbosity directly from the command line. The `adk web`

, `adk api_server`

, and `adk deploy cloud_run`

commands all accept a `--log_level`

option.

This provides a convenient way to set the logging level without modifying your agent's source code.


Note:The command-line setting always takes precedence over the programmatic configuration (like`logging.basicConfig`

) for ADK's loggers. It's recommended to use`INFO`

or`WARNING`

in production and enable`DEBUG`

only when troubleshooting.

**Example using adk web:**

To start the web server with `DEBUG`

level logging, run:

The available log levels for the `--log_level`

option are:

`DEBUG`

`INFO`

(default)`WARNING`

`ERROR`

`CRITICAL`


You can also use

`-v`

or`--verbose`

as a shortcut for`--log_level DEBUG`

.

### Log Levels[¶](#log-levels)

ADK uses standard log levels to categorize messages. The configured level determines what information gets logged.

| Level | Description | Type of Information Logged |
|---|---|---|
`DEBUG` |
Crucial for debugging. The most verbose level for fine-grained diagnostic information. |
|
`INFO` |
General information about the agent's lifecycle. |
|
`WARNING` |
Indicates a potential issue or deprecated feature use. The agent continues to function, but attention may be required. |
|
`ERROR` |
A serious error that prevented an operation from completing. |
|


Note:It is recommended to use`INFO`

or`WARNING`

in production environments. Only enable`DEBUG`

when actively troubleshooting an issue, as`DEBUG`

logs can be very verbose and may contain sensitive information.

## Reading and Understanding the Logs[¶](#reading-and-understanding-the-logs)

The `format`

string in the `basicConfig`

example determines the structure of each log message.

Here’s a sample log entry:

2025-07-08 11:22:33,456 - DEBUG - google_adk.google.adk.models.google_llm - LLM Request: contents { ... }


| Log Segment | Format Specifier | Meaning |
|---|---|---|
`2025-07-08 11:22:33,456` |
`%(asctime)s` |
Timestamp |
`DEBUG` |
`%(levelname)s` |
Severity level |
`google_adk.models.google_llm` |
`%(name)s` |
Logger name (the module that produced the log) |
`LLM Request: contents { ... }` |
`%(message)s` |
The actual log message |

By reading the logger name, you can immediately pinpoint the source of the log and understand its context within the agent's architecture.

## Debugging with Logs: A Practical Example[¶](#debugging-with-logs-a-practical-example)

**Scenario:** Your agent is not producing the expected output, and you suspect the prompt being sent to the LLM is incorrect or missing information.

**Steps:**

-
**Enable DEBUG Logging:**In your`main.py`

, set the logging level to`DEBUG`

as shown in the configuration example. -
**Run Your Agent:**Execute your agent's task as you normally would. -
**Inspect the Logs:**Look through the console output for a message from the`google.adk.models.google_llm`

logger that starts with`LLM Request:`

.[...](#__codelineno-5-1)[2025-07-10 15:26:13,778 - DEBUG - google_adk.google.adk.models.google_llm - Sending out request, model: gemini-2.0-flash, backend: GoogleLLMVariant.GEMINI_API, stream: False](#__codelineno-5-2)[2025-07-10 15:26:13,778 - DEBUG - google_adk.google.adk.models.google_llm -](#__codelineno-5-3)[LLM Request:](#__codelineno-5-4)[-----------------------------------------------------------](#__codelineno-5-5)[System Instruction:](#__codelineno-5-6)[You roll dice and answer questions about the outcome of the dice rolls.](#__codelineno-5-8)[You can roll dice of different sizes.](#__codelineno-5-9)[You can use multiple tools in parallel by calling functions in parallel(in one request and in one round).](#__codelineno-5-10)[It is ok to discuss previous dice roles, and comment on the dice rolls.](#__codelineno-5-11)[When you are asked to roll a die, you must call the roll_die tool with the number of sides. Be sure to pass in an integer. Do not pass in a string.](#__codelineno-5-12)[You should never roll a die on your own.](#__codelineno-5-13)[When checking prime numbers, call the check_prime tool with a list of integers. Be sure to pass in a list of integers. You should never pass in a string.](#__codelineno-5-14)[You should not check prime numbers before calling the tool.](#__codelineno-5-15)[When you are asked to roll a die and check prime numbers, you should always make the following two function calls:](#__codelineno-5-16)[1. You should first call the roll_die tool to get a roll. Wait for the function response before calling the check_prime tool.](#__codelineno-5-17)[2. After you get the function response from roll_die tool, you should call the check_prime tool with the roll_die result.](#__codelineno-5-18)[2.1 If user asks you to check primes based on previous rolls, make sure you include the previous rolls in the list.](#__codelineno-5-19)[3. When you respond, you must include the roll_die result from step 1.](#__codelineno-5-20)[You should always perform the previous 3 steps when asking for a roll and checking prime numbers.](#__codelineno-5-21)[You should not rely on the previous history on prime results.](#__codelineno-5-22)[You are an agent. Your internal name is "hello_world_agent".](#__codelineno-5-25)[The description about you is "hello world agent that can roll a dice of 8 sides and check prime numbers."](#__codelineno-5-27)[-----------------------------------------------------------](#__codelineno-5-28)[Contents:](#__codelineno-5-29)[{"parts":[{"text":"Roll a 6 sided dice"}],"role":"user"}](#__codelineno-5-30)[{"parts":[{"function_call":{"args":{"sides":6},"name":"roll_die"}}],"role":"model"}](#__codelineno-5-31)[{"parts":[{"function_response":{"name":"roll_die","response":{"result":2}}}],"role":"user"}](#__codelineno-5-32)[-----------------------------------------------------------](#__codelineno-5-33)[Functions:](#__codelineno-5-34)[roll_die: {'sides': {'type': <Type.INTEGER: 'INTEGER'>}}](#__codelineno-5-35)[check_prime: {'nums': {'items': {'type': <Type.INTEGER: 'INTEGER'>}, 'type': <Type.ARRAY: 'ARRAY'>}}](#__codelineno-5-36)[-----------------------------------------------------------](#__codelineno-5-37)[2025-07-10 15:26:13,779 - INFO - google_genai.models - AFC is enabled with max remote calls: 10.](#__codelineno-5-39)[2025-07-10 15:26:14,309 - INFO - google_adk.google.adk.models.google_llm -](#__codelineno-5-40)[LLM Response:](#__codelineno-5-41)[-----------------------------------------------------------](#__codelineno-5-42)[Text:](#__codelineno-5-43)[I have rolled a 6 sided die, and the result is 2.](#__codelineno-5-44)[...](#__codelineno-5-45) -
**Analyze the Prompt:**By examining the`System Instruction`

,`contents`

,`functions`

sections of the logged request, you can verify:- Is the system instruction correct?
- Is the conversation history (
`user`

and`model`

turns) accurate? - Is the most recent user query included?
- Are the correct tools being provided to the model?
- Are the tools correctly called by the model?
- How long it takes for the model to respond?


This detailed output allows you to diagnose a wide range of issues, from incorrect prompt engineering to problems with tool definitions, directly from the log files.