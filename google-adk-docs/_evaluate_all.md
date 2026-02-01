---
merged_at: 2026-02-01T07:57:00.001749
merged_files: 3
---


---
<!-- Source: https://google.github.io/adk-docs/evaluate/user-sim/ -->

# User Simulation¶

# User Simulation[¶](#user-simulation)

When evaluating conversational agents, it is not always practical to use a fixed set of user prompts, as the conversation can proceed in unexpected ways. For example, if the agent needs the user to supply two values to perform a task, it may ask for those values one at a time or both at once. To resolve this issue, ADK can dynamically generate user prompts using a generative AI model.

To use this feature, you must specify a
[ ConversationScenario](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/conversation_scenarios.py)
which dictates the user's goals in their conversation with the agent.
A sample conversation scenario for the

[agent is shown below:](https://github.com/google/adk-python/tree/main/contributing/samples/hello_world)

`hello_world`

{
"starting_prompt": "What can you do for me?",
"conversation_plan": "Ask the agent to roll a 20-sided die. After you get the result, ask the agent to check if it is prime."
}


The `starting_prompt`

in a conversation scenario specifies a fixed initial
prompt that the user should use to start the conversation with the agent.
Specifying such fixed prompts for subsequent interactions with the agent is not
practical as the agent may respond in different ways.
Instead, the `conversation_plan`

provides a guideline for how the rest of the
conversation with the agent should proceed.
An LLM uses this conversation plan, along with the conversation history, to
dynamically generate user prompts until it judges that the conversation is
complete.

Try it in Colab

Test this entire workflow yourself in an interactive notebook on
[Simulating User Conversations to Dynamically Evaluate ADK Agents](https://github.com/google/adk-samples/blob/main/python/notebooks/evaluation/user_simulation_in_adk_evals.ipynb).
You'll define a conversation scenario, run a "dry run" to check the
dialogue, and then perform a full evaluation to score the agent's responses.

## Example: Evaluating the `hello_world`

agent with conversation scenarios[¶](#example-evaluating-the-hello_world-agent-with-conversation-scenarios)

`hello_world`

To add evaluation cases containing conversation scenarios to a new or existing
[ EvalSet](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_set.py),
you need to first create a list of conversation scenarios to test the agent in.

Try saving the following to
`contributing/samples/hello_world/conversation_scenarios.json`

:

{
"scenarios": [
{
"starting_prompt": "What can you do for me?",
"conversation_plan": "Ask the agent to roll a 20-sided die. After you get the result, ask the agent to check if it is prime."
},
{
"starting_prompt": "Hi, I'm running a tabletop RPG in which prime numbers are bad!",
"conversation_plan": "Say that you don't care about the value; you just want the agent to tell you if a roll is good or bad. Once the agent agrees, ask it to roll a 6-sided die. Finally, ask the agent to do the same with 2 20-sided dice."
}
]
}


You will also need a session input file containing information used during
evaluation.
Try saving the following to
`contributing/samples/hello_world/session_input.json`

:

Then, you can add the conversation scenarios to an `EvalSet`

:

# (optional) create a new EvalSet
adk eval_set create \
contributing/samples/hello_world \
eval_set_with_scenarios
# add conversation scenarios to the EvalSet as new eval cases
adk eval_set add_eval_case \
contributing/samples/hello_world \
eval_set_with_scenarios \
--scenarios_file contributing/samples/hello_world/conversation_scenarios.json \
--session_input_file contributing/samples/hello_world/session_input.json


By default, ADK runs evaluations with metrics that require the agent's expected
response to be specified.
Since that is not the case for a dynamic conversation scenario, we will use an
[ EvalConfig](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_config.py)
with some alternate supported metrics.

Try saving the following to
`contributing/samples/hello_world/eval_config.json`

:

{
"criteria": {
"hallucinations_v1": {
"threshold": 0.5,
"evaluate_intermediate_nl_responses": true
},
"safety_v1": {
"threshold": 0.8
}
}
}


Finally, you can use the `adk eval`

command to run the evaluation:

adk eval \
contributing/samples/hello_world \
--config_file_path contributing/samples/hello_world/eval_config.json \
eval_set_with_scenarios \
--print_detailed_results


## User simulator configuration[¶](#user-simulator-configuration)

You can override the default user simulator configuration to change the model,
internal model behavior, and the maximum number of user-agent interactions.
The below `EvalConfig`

shows the default user simulator configuration:

{
"criteria": {
# same as before
},
"user_simulator_config": {
"model": "gemini-2.5-flash",
"model_configuration": {
"thinking_config": {
"include_thoughts": true,
"thinking_budget": 10240
}
},
"max_allowed_invocations": 20
}
}


`model`

: The model backing the user simulator.`model_configuration`

: Awhich controls the model behavior.`GenerateContentConfig`

`max_allowed_invocations`

: The maximum user-agent interactions allowed before the conversation is forcefully terminated. This should be set to be greater than the longest reasonable user-agent interaction in your`EvalSet`

.

---
<!-- Source: https://google.github.io/adk-docs/evaluate/criteria/ -->

# Evaluation Criteria¶

# Evaluation Criteria[¶](#evaluation-criteria)

This page outlines the evaluation criteria provided by ADK to assess agent performance, including tool use trajectory, response quality, and safety.

| Criterion | Description | Reference-Based | Requires Rubrics | LLM-as-a-Judge | Supports
|
|---|

`tool_trajectory_avg_score`

`response_match_score`

`final_response_match_v2`

`rubric_based_final_response_quality_v1`

`rubric_based_tool_use_quality_v1`

`hallucinations_v1`

`safety_v1`

`per_turn_user_simulator_quality_v1`

## tool_trajectory_avg_score[¶](#tool_trajectory_avg_score)

This criterion compares the sequence of tools called by the agent against a list
of expected calls and computes an average score based on one of the match types:
`EXACT`

, `IN_ORDER`

, or `ANY_ORDER`

.

#### When To Use This Criterion?[¶](#when-to-use-this-criterion)

This criterion is ideal for scenarios where agent correctness depends on tool
calls. Depending on how strictly tool calls need to be followed, you can choose
from one of three match types: `EXACT`

, `IN_ORDER`

, and `ANY_ORDER`

.

This metric is particularly valuable for:

**Regression testing:**Ensuring that agent updates do not unintentionally alter tool call behavior for established test cases.**Workflow validation:**Verifying that agents correctly follow predefined workflows that require specific API calls in a specific order.**High-precision tasks:**Evaluating tasks where slight deviations in tool parameters or call order can lead to significantly different or incorrect outcomes.

Use `EXACT`

match when you need to enforce a specific tool execution path and
consider any deviation—whether in tool name, arguments, or order—as a failure.

Use `IN_ORDER`

match when you want to ensure certain key tool calls occur in a
specific order, but allow for other tool calls to happen in between. This option is
useful in assuring if certain key actions or tool calls occur and in certain order,
leaving some scope for other tools calls to happen as well.

Use `ANY_ORDER`

match when you want to ensure certain key tool calls occur, but
do not care about their order, and allow for other tool calls to happen in
between. This criteria is helpful for cases where multiple tool calls about the
same concept occur, like your agent issues 5 search queries. You don't really
care the order in which the search queries are issued, till they occur.

#### Details[¶](#details)

For each invocation that is being evaluated, this criterion compares the list of tool calls produced by the agent against the list of expected tool calls using one of three match types. If the tool calls match based on the selected match type, a score of 1.0 is awarded for that invocation, otherwise the score is 0.0. The final value is the average of these scores across all invocations in the eval case.

The comparison can be done using one of following match types:

: Requires a perfect match between the actual and expected tool calls, with no extra or missing tool calls.`EXACT`

: Requires all tool calls from the expected list to be present in the actual list, in the same order, but allows for other tool calls to appear in between.`IN_ORDER`

: Requires all tool calls from the expected list to be present in the actual list, in any order, and allows for other tool calls to appear in between.`ANY_ORDER`


#### How To Use This Criterion?[¶](#how-to-use-this-criterion)

By default, `tool_trajectory_avg_score`

uses `EXACT`

match type. You can specify
just a threshold for this criterion in `EvalConfig`

under the `criteria`

dictionary for `EXACT`

match type. The value should be a float between 0.0 and
1.0, which represents the minimum acceptable score for the eval case to pass. If
you expect tool trajectories to match exactly in all invocations, you should set
the threshold to 1.0.

Example `EvalConfig`

entry for `EXACT`

match:

Or you could specify the `match_type`

explicitly:

If you want to use `IN_ORDER`

or `ANY_ORDER`

match type, you can specify it via
`match_type`

field along with threshold.

Example `EvalConfig`

entry for `IN_ORDER`

match:

Example `EvalConfig`

entry for `ANY_ORDER`

match:

#### Output And How To Interpret[¶](#output-and-how-to-interpret)

The output is a score between 0.0 and 1.0, where 1.0 indicates a perfect match between actual and expected tool trajectories for all invocations, and 0.0 indicates a complete mismatch for all invocations. Higher scores are better. A score below 1.0 means that for at least one invocation, the agent's tool call trajectory deviated from the expected one.

## response_match_score[¶](#response_match_score)

This criterion evaluates if agent's final response matches a golden/expected final response using Rouge-1.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_1)

Use this criterion when you need a quantitative measure of how closely the agent's output matches the expected output in terms of content overlap.

### Details[¶](#details_1)

ROUGE-1 specifically measures the overlap of unigrams (single words) between the
system-generated text (candidate summary) and the a reference text. It
essentially checks how many individual words from the reference text are present
in the candidate text. To learn more, see details on
[ROUGE-1](https://github.com/google-research/google-research/tree/master/rouge).

### How To Use This Criterion?[¶](#how-to-use-this-criterion_1)

You can specify a threshold for this criterion in `EvalConfig`

under the
`criteria`

dictionary. The value should be a float between 0.0 and 1.0, which
represents the minimum acceptable score for the eval case to pass.

Example `EvalConfig`

entry:

### Output And How To Interpret[¶](#output-and-how-to-interpret_1)

Value range for this criterion is [0,1], with values closer to 1 more desirable.

## final_response_match_v2[¶](#final_response_match_v2)

This criterion evaluates if the agent's final response matches a golden/expected final response using LLM as a judge.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_2)

Use this criterion when you need to evaluate the correctness of an agent's final
response against a reference, but require flexibility in how the answer is
presented. It is suitable for cases where different phrasings or formats are
acceptable, as long as the core meaning and information match the reference.
This criterion is a good choice for evaluating question-answering,
summarization, or other generative tasks where semantic equivalence is more
important than exact lexical overlap, making it a more sophisticated alternative
to `response_match_score`

.

### Details[¶](#details_2)

This criterion uses a Large Language Model (LLM) as a judge to determine if the
agent's final response is semantically equivalent to the provided reference
response. It is designed to be more flexible than lexical matching metrics (like
`response_match_score`

), as it focuses on whether the agent's response contains
the correct information, while tolerating differences in formatting, phrasing,
or the inclusion of additional correct details.

For each invocation, the criterion prompts a judge LLM to rate the agent's
response as "valid" or "invalid" compared to the reference. This is repeated
multiple times for robustness (configurable via `num_samples`

), and a majority
vote determines if the invocation receives a score of 1.0 (valid) or 0.0
(invalid). The final criterion score is the fraction of invocations deemed valid
across the entire eval case.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_2)

This criterion uses `LlmAsAJudgeCriterion`

, allowing you to configure the
evaluation threshold, the judge model, and the number of samples per invocation.

Example `EvalConfig`

entry:

{
"criteria": {
"final_response_match_v2": {
"threshold": 0.8,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
}
}
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_2)

The criterion returns a score between 0.0 and 1.0. A score of 1.0 means the LLM judge considered the agent's final response to be valid for all invocations, while a score closer to 0.0 indicates that many responses were judged as invalid when compared to the reference responses. Higher values are better.

## rubric_based_final_response_quality_v1[¶](#rubric_based_final_response_quality_v1)

This criterion assesses the quality of an agent's final response against a user-defined set of rubrics using LLM as a judge.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_3)

Use this criterion when you need to evaluate aspects of response quality that go beyond simple correctness or semantic equivalence with a reference. It is ideal for assessing nuanced attributes like tone, style, helpfulness, or adherence to specific conversational guidelines defined in your rubrics. This criterion is particularly useful when no single reference response exists, or when quality depends on multiple subjective factors.

### Details[¶](#details_3)

This criterion provides a flexible way to evaluate response quality based on specific criteria that you define as rubrics. For example, you could define rubrics to check if a response is concise, if it correctly infers user intent, or if it avoids jargon.

The criterion uses an LLM-as-a-judge to evaluate the agent's final response
against each rubric, producing a `yes`

(1.0) or `no`

(0.0) verdict for each.
Like other LLM-based metrics, it samples the judge model multiple times per
invocation and uses a majority vote to determine the score for each rubric in
that invocation. The overall score for an invocation is the average of its
rubric scores. The final criterion score for the eval case is the average of
these overall scores across all invocations.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_3)

This criterion uses `RubricsBasedCriterion`

, which requires a list of rubrics to
be provided in the `EvalConfig`

. Each rubric should be defined with a unique ID
and its content.

Example `EvalConfig`

entry:

{
"criteria": {
"rubric_based_final_response_quality_v1": {
"threshold": 0.8,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
},
"rubrics": [
{
"rubric_id": "conciseness",
"rubric_content": {
"text_property": "The agent's response is direct and to the point."
}
},
{
"rubric_id": "intent_inference",
"rubric_content": {
"text_property": "The agent's response accurately infers the user's underlying goal from ambiguous queries."
}
}
]
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_3)

The criterion outputs an overall score between 0.0 and 1.0, where 1.0 indicates that the agent's responses satisfied all rubrics across all invocations, and 0.0 indicates that no rubrics were satisfied. The results also include detailed per-rubric scores for each invocation. Higher values are better.

## rubric_based_tool_use_quality_v1[¶](#rubric_based_tool_use_quality_v1)

This criterion assesses the quality of an agent's tool usage against a user-defined set of rubrics using LLM as a judge.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_4)

Use this criterion when you need to evaluate *how* an agent uses tools, rather
than just *if* the final response is correct. It is ideal for assessing whether
the agent selected the right tool, used the correct parameters, or followed a
specific sequence of tool calls. This is useful for validating agent reasoning
processes, debugging tool-use errors, and ensuring adherence to prescribed
workflows, especially in cases where multiple tool-use paths could lead to a
similar final answer but only one path is considered correct.

### Details[¶](#details_4)

This criterion provides a flexible way to evaluate tool usage based on specific rules that you define as rubrics. For example, you could define rubrics to check if a specific tool was called, if its parameters were correct, or if tools were called in a particular order.

The criterion uses an LLM-as-a-judge to evaluate the agent's tool calls and
responses against each rubric, producing a `yes`

(1.0) or `no`

(0.0) verdict for
each. Like other LLM-based metrics, it samples the judge model multiple times
per invocation and uses a majority vote to determine the score for each rubric
in that invocation. The overall score for an invocation is the average of its
rubric scores. The final criterion score for the eval case is the average of
these overall scores across all invocations.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_4)

This criterion uses `RubricsBasedCriterion`

, which requires a list of rubrics to
be provided in the `EvalConfig`

. Each rubric should be defined with a unique ID
and its content, describing a specific aspect of tool use to evaluate.

Example `EvalConfig`

entry:

{
"criteria": {
"rubric_based_tool_use_quality_v1": {
"threshold": 1.0,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
},
"rubrics": [
{
"rubric_id": "geocoding_called",
"rubric_content": {
"text_property": "The agent calls the GeoCoding tool before calling the GetWeather tool."
}
},
{
"rubric_id": "getweather_called",
"rubric_content": {
"text_property": "The agent calls the GetWeather tool with coordinates derived from the user's location."
}
}
]
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_4)

The criterion outputs an overall score between 0.0 and 1.0, where 1.0 indicates that the agent's tool usage satisfied all rubrics across all invocations, and 0.0 indicates that no rubrics were satisfied. The results also include detailed per-rubric scores for each invocation. Higher values are better.

## hallucinations_v1[¶](#hallucinations_v1)

This criterion assesses whether a model response contains any false, contradictory, or unsupported claims.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_5)

Use this criterion to ensure the agent's response is grounded in the provided context (e.g., tool outputs, user query, instructions) and does not contain hallucinations.

### Details[¶](#details_5)

This criterion assesses whether a model response contains any false, contradictory, or unsupported claims based on context that includes developer instructions, user prompt, tool definitions, and tool invocations and their results. It uses LLM-as-a-judge and follows a two-step process:

**Segmenter**: Segments the agent response into individual sentences.**Sentence Validator**: Evaluates each segmented sentence against the provided context for grounding. Each sentence is labeled as`supported`

,`unsupported`

,`contradictory`

,`disputed`

or`not_applicable`

.

The metric computes an Accuracy Score: the percentage of sentences that are
`supported`

or `not_applicable`

. By default, only the final response is
evaluated. If `evaluate_intermediate_nl_responses`

is set to true in the
criterion, intermediate natural language responses from agents are also
evaluated.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_5)

This criterion uses `HallucinationsCriterion`

, allowing you to configure the
evaluation threshold, the judge model, the number of samples per invocation and
whether to evaluate intermediate natural language responses.

Example `EvalConfig`

entry:

{
"criteria": {
"hallucinations_v1": {
"threshold": 0.8,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
},
"evaluate_intermediate_nl_responses": true
}
}
}


### Output And How To Interpret[¶](#output-and-how-to-interpret_5)

The criterion returns a score between 0.0 and 1.0. A score of 1.0 means all sentences in agent's response are grounded in the context, while a score closer to 0.0 indicates that many sentences are false, contradictory, or unsupported. Higher values are better.

## safety_v1[¶](#safety_v1)

This criterion evaluates the safety (harmlessness) of an Agent's Response.

### When To Use This Criterion?[¶](#when-to-use-this-criterion_6)

This criterion should be used when you need to ensure that agent responses comply with safety guidelines and do not produce harmful or inappropriate content. It is essential for user-facing applications or any system where response safety is a priority.

### Details[¶](#details_6)

This criterion assesses whether the agent's response contains any harmful
content, such as hate speech, harassment, or dangerous information. Unlike other
metrics implemented natively within ADK, `safety_v1`

delegates the evaluation to
the Vertex AI General AI Eval SDK.

### How To Use This Criterion?[¶](#how-to-use-this-criterion_6)

Using this criterion requires a Google Cloud Project. You must have
`GOOGLE_CLOUD_PROJECT`

and `GOOGLE_CLOUD_LOCATION`

environment variables set,
typically in an `.env`

file in your agent's directory, for the Vertex AI SDK to
function correctly.

You can specify a threshold for this criterion in `EvalConfig`

under the
`criteria`

dictionary. The value should be a float between 0.0 and 1.0,
representing the minimum safety score for a response to be considered passing.

Example `EvalConfig`

entry:

### Output And How To Interpret[¶](#output-and-how-to-interpret_6)

The criterion returns a score between 0.0 and 1.0. Scores closer to 1.0 indicate that the response is safe, while scores closer to 0.0 indicate potential safety issues.

## per_turn_user_simulator_quality_v1[¶](#per_turn_user_simulator_quality_v1)

This criterion evaluates whether a user simulator is faithful to a conversation plan.

#### When To Use This Criterion?[¶](#when-to-use-this-criterion_7)

Use this criterion when you need to evaluate a user simulator in a multi-turn
conversation. It is designed to assess whether the simulator follows the
conversation plan defined in the `ConversationScenario`

.

#### Details[¶](#details_7)

This criterion determines whether the a user simulator follows a defined
`ConversationScenario`

in a multi-turn conversation.

For the first turn, this criterion checks if user simulator response matches the
`starting_prompt`

in the `ConversationScenario`

. For subsequent turns, it uses
LLM-as-a-judge to evaluate if the user response follows the `conversation_plan`

in the `ConversationScenario`

.

#### How To Use This Criterion?[¶](#how-to-use-this-criterion_7)

This criterion allows you to configure the evaluation threshold, the judge model
and the number of samples per invocation. The criterion also lets you specify a
`stop_signal`

, which signals the LLM judge that the conversation was completed.
For best results, use the stop signal in `LlmBackedUserSimulator`

.

Example `EvalConfig`

entry:

{
"criteria": {
"per_turn_user_simulator_quality_v1": {
"threshold": 1.0,
"judge_model_options": {
"judge_model": "gemini-2.5-flash",
"num_samples": 5
},
"stop_signal": "</finished>"
}
}
}


#### Output And How To Interpret[¶](#output-and-how-to-interpret_7)

The criterion returns a score between 0.0 and 1.0, representing the fraction of turns in which the user simulator's response was judged to be valid according to the conversation scenario. A score of 1.0 indicates that the simulator behaved as expected in all turns, while a score closer to 0.0 indicates that the simulator deviated in many turns. Higher values are better.

---
<!-- Source: https://google.github.io/adk-docs/evaluate/ -->

# Why Evaluate Agents¶

# Why Evaluate Agents[¶](#why-evaluate-agents)

In traditional software development, unit tests and integration tests provide confidence that code functions as expected and remains stable through changes. These tests provide a clear "pass/fail" signal, guiding further development. However, LLM agents introduce a level of variability that makes traditional testing approaches insufficient.

Due to the probabilistic nature of models, deterministic "pass/fail" assertions are often unsuitable for evaluating agent performance. Instead, we need qualitative evaluations of both the final output and the agent's trajectory - the sequence of steps taken to reach the solution. This involves assessing the quality of the agent's decisions, its reasoning process, and the final result.

This may seem like a lot of extra work to set up, but the investment of automating evaluations pays off quickly. If you intend to progress beyond prototype, this is a highly recommended best practice.

## Preparing for Agent Evaluations[¶](#preparing-for-agent-evaluations)

Before automating agent evaluations, define clear objectives and success criteria:

**Define Success:**What constitutes a successful outcome for your agent?**Identify Critical Tasks:**What are the essential tasks your agent must accomplish?**Choose Relevant Metrics:**What metrics will you track to measure performance?

These considerations will guide the creation of evaluation scenarios and enable effective monitoring of agent behavior in real-world deployments.

## What to Evaluate?[¶](#what-to-evaluate)

To bridge the gap between a proof-of-concept and a production-ready AI agent, a robust and automated evaluation framework is essential. Unlike evaluating generative models, where the focus is primarily on the final output, agent evaluation requires a deeper understanding of the decision-making process. Agent evaluation can be broken down into two components:

**Evaluating Trajectory and Tool Use:**Analyzing the steps an agent takes to reach a solution, including its choice of tools, strategies, and the efficiency of its approach.**Evaluating the Final Response:**Assessing the quality, relevance, and correctness of the agent's final output.

The trajectory is just a list of steps the agent took before it returned to the user. We can compare that against the list of steps we expect the agent to have taken.

### Evaluating trajectory and tool use[¶](#evaluating-trajectory-and-tool-use)

Before responding to a user, an agent typically performs a series of actions, which we refer to as a 'trajectory.' It might compare the user input with session history to disambiguate a term, or lookup a policy document, search a knowledge base or invoke an API to save a ticket. We call this a ‘trajectory’ of actions. Evaluating an agent's performance requires comparing its actual trajectory to an expected, or ideal, one. This comparison can reveal errors and inefficiencies in the agent's process. The expected trajectory represents the ground truth -- the list of steps we anticipate the agent should take.

For example:

# Trajectory evaluation will compare
expected_steps = ["determine_intent", "use_tool", "review_results", "report_generation"]
actual_steps = ["determine_intent", "use_tool", "review_results", "report_generation"]


ADK provides both groundtruth based and rubric based tool use evaluation metrics. To select the appropriate metric for your agent's specific requirements and goals, please refer to our [recommendations](#recommendations-on-criteria).

## How Evaluation works with the ADK[¶](#how-evaluation-works-with-the-adk)

The ADK offers two methods for evaluating agent performance against predefined datasets and evaluation criteria. While conceptually similar, they differ in the amount of data they can process, which typically dictates the appropriate use case for each.

### First approach: Using a test file[¶](#first-approach-using-a-test-file)

This approach involves creating individual test files, each representing a single, simple agent-model interaction (a session). It's most effective during active agent development, serving as a form of unit testing. These tests are designed for rapid execution and should focus on simple session complexity. Each test file contains a single session, which may consist of multiple turns. A turn represents a single interaction between the user and the agent. Each turn includes

`User Content`

: The user issued query.`Expected Intermediate Tool Use Trajectory`

: The tool calls we expect the agent to make in order to respond correctly to the user query.`Expected Intermediate Agent Responses`

: These are the natural language responses that the agent (or sub-agents) generates as it moves towards generating a final answer. These natural language responses are usually an artifact of an multi-agent system, where your root agent depends on sub-agents to achieve a goal. These intermediate responses, may or may not be of interest to the end user, but for a developer/owner of the system, are of critical importance, as they give you the confidence that the agent went through the right path to generate final response.`Final Response`

: The expected final response from the agent.

You can give the file any name for example `evaluation.test.json`

. The framework only checks for the `.test.json`

suffix, and the preceding part of the filename is not constrained. The test files are backed by a formal Pydantic data model. The two key schema files are
[Eval Set](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_set.py) and
[Eval Case](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_case.py).
Here is a test file with a few examples:

*(Note: Comments are included for explanatory purposes and should be removed for the JSON to be valid.)*

# Do note that some fields are removed for sake of making this doc readable.
{
"eval_set_id": "home_automation_agent_light_on_off_set",
"name": "",
"description": "This is an eval set that is used for unit testing `x` behavior of the Agent",
"eval_cases": [
{
"eval_id": "eval_case_id",
"conversation": [
{
"invocation_id": "b7982664-0ab6-47cc-ab13-326656afdf75", # Unique identifier for the invocation.
"user_content": { # Content provided by the user in this invocation. This is the query.
"parts": [
{
"text": "Turn off device_2 in the Bedroom."
}
],
"role": "user"
},
"final_response": { # Final response from the agent that acts as a reference of benchmark.
"parts": [
{
"text": "I have set the device_2 status to off."
}
],
"role": "model"
},
"intermediate_data": {
"tool_uses": [ # Tool use trajectory in chronological order.
{
"args": {
"location": "Bedroom",
"device_id": "device_2",
"status": "OFF"
},
"name": "set_device_info"
}
],
"intermediate_responses": [] # Any intermediate sub-agent responses.
}
}
],
"session_input": { # Initial session input.
"app_name": "home_automation_agent",
"user_id": "test_user",
"state": {}
}
}
]
}


Test files can be organized into folders. Optionally, a folder can also include a `test_config.json`

file that specifies the evaluation criteria.

#### How to migrate test files not backed by the Pydantic schema?[¶](#how-to-migrate-test-files-not-backed-by-the-pydantic-schema)

NOTE: If your test files don't adhere to [EvalSet](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_set.py) schema file, then this section is relevant to you.

Please use `AgentEvaluator.migrate_eval_data_to_new_schema`

to migrate your
existing `*.test.json`

files to the Pydantic backed schema.

The utility takes your current test data file and an optional initial session file, and generates a single output json file with data serialized in the new format. Given that the new schema is more cohesive, both the old test data file and initial session file can be ignored (or removed.)

### Second approach: Using An Evalset File[¶](#second-approach-using-an-evalset-file)

The evalset approach utilizes a dedicated dataset called an "evalset" for evaluating agent-model interactions. Similar to a test file, the evalset contains example interactions. However, an evalset can contain multiple, potentially lengthy sessions, making it ideal for simulating complex, multi-turn conversations. Due to its ability to represent complex sessions, the evalset is well-suited for integration tests. These tests are typically run less frequently than unit tests due to their more extensive nature.

An evalset file contains multiple "evals," each representing a distinct session. Each eval consists of one or more "turns," which include the user query, expected tool use, expected intermediate agent responses, and a reference response. These fields have the same meaning as they do in the test file approach. Alternatively, an eval can define a *conversation scenario* which is used to [dynamically simulate](user-sim/) a user interaction with the agent. Each eval is identified by a unique name. Furthermore, each eval includes an associated initial session state.

Creating evalsets manually can be complex, therefore UI tools are provided to help capture relevant sessions and easily convert them into evals within your evalset. Learn more about using the web UI for evaluation below. Here is an example evalset containing two sessions. The eval set files are backed by a formal Pydantic data model. The two key schema files are
[Eval Set](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_set.py) and
[Eval Case](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_case.py).

Warning

This evalset evaluation method requires the use of a paid service,
[Vertex Gen AI Evaluation Service API](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/evaluation).

*(Note: Comments are included for explanatory purposes and should be removed for the JSON to be valid.)*

# Do note that some fields are removed for sake of making this doc readable.
{
"eval_set_id": "eval_set_example_with_multiple_sessions",
"name": "Eval set with multiple sessions",
"description": "This eval set is an example that shows that an eval set can have more than one session.",
"eval_cases": [
{
"eval_id": "session_01",
"conversation": [
{
"invocation_id": "e-0067f6c4-ac27-4f24-81d7-3ab994c28768",
"user_content": {
"parts": [
{
"text": "What can you do?"
}
],
"role": "user"
},
"final_response": {
"parts": [
{
"text": "I can roll dice of different sizes and check if numbers are prime."
}
],
"role": null
},
"intermediate_data": {
"tool_uses": [],
"intermediate_responses": []
}
}
],
"session_input": {
"app_name": "hello_world",
"user_id": "user",
"state": {}
}
},
{
"eval_id": "session_02",
"conversation": [
{
"invocation_id": "e-92d34c6d-0a1b-452a-ba90-33af2838647a",
"user_content": {
"parts": [
{
"text": "Roll a 19 sided dice"
}
],
"role": "user"
},
"final_response": {
"parts": [
{
"text": "I rolled a 17."
}
],
"role": null
},
"intermediate_data": {
"tool_uses": [],
"intermediate_responses": []
}
},
{
"invocation_id": "e-bf8549a1-2a61-4ecc-a4ee-4efbbf25a8ea",
"user_content": {
"parts": [
{
"text": "Roll a 10 sided dice twice and then check if 9 is a prime or not"
}
],
"role": "user"
},
"final_response": {
"parts": [
{
"text": "I got 4 and 7 from the dice roll, and 9 is not a prime number.\n"
}
],
"role": null
},
"intermediate_data": {
"tool_uses": [
{
"id": "adk-1a3f5a01-1782-4530-949f-07cf53fc6f05",
"args": {
"sides": 10
},
"name": "roll_die"
},
{
"id": "adk-52fc3269-caaf-41c3-833d-511e454c7058",
"args": {
"sides": 10
},
"name": "roll_die"
},
{
"id": "adk-5274768e-9ec5-4915-b6cf-f5d7f0387056",
"args": {
"nums": [
9
]
},
"name": "check_prime"
}
],
"intermediate_responses": [
[
"data_processing_agent",
[
{
"text": "I have rolled a 10 sided die twice. The first roll is 5 and the second roll is 3.\n"
}
]
]
]
}
}
],
"session_input": {
"app_name": "hello_world",
"user_id": "user",
"state": {}
}
}
]
}


#### How to migrate eval set files not backed by the Pydantic schema?[¶](#how-to-migrate-eval-set-files-not-backed-by-the-pydantic-schema)

NOTE: If your eval set files don't adhere to [EvalSet](https://github.com/google/adk-python/blob/main/src/google/adk/evaluation/eval_set.py) schema file, then this section is relevant to you.

Based on who is maintaining the eval set data, there are two routes:

-
**Eval set data maintained by ADK UI**If you use ADK UI to maintain your Eval set data then*no action is needed*from you. -
**Eval set data is developed and maintained manually and used in ADK eval CLI**A migration tool is in the works, until then the ADK eval CLI command will continue to support data in the old format.

### Evaluation Criteria[¶](#evaluation-criteria)

ADK provides several built-in criteria for evaluating agent performance, ranging
from tool trajectory matching to LLM-based response quality assessment. For a
detailed list of available criteria and guidance on when to use them, please see
[Evaluation Criteria](criteria/).

Here is a summary of all the available criteria:

**tool_trajectory_avg_score**: Exact match of tool call trajectory.**response_match_score**: ROUGE-1 similarity to reference response.**final_response_match_v2**: LLM-judged semantic match to a reference response.**rubric_based_final_response_quality_v1**: LLM-judged final response quality based on custom rubrics.**rubric_based_tool_use_quality_v1**: LLM-judged tool usage quality based on custom rubrics.**hallucinations_v1**: LLM-judged groundedness of agent response against context.**safety_v1**: Safety/harmlessness of agent response.

If no evaluation criteria are provided, the following default configuration is used:

`tool_trajectory_avg_score`

: Defaults to 1.0, requiring a 100% match in the tool usage trajectory.`response_match_score`

: Defaults to 0.8, allowing for a small margin of error in the agent's natural language responses.

Here is an example of a `test_config.json`

file specifying custom evaluation criteria:

#### Recommendations on Criteria[¶](#recommendations-on-criteria)

Choose criteria based on your evaluation goals:

**Enable tests in CI/CD pipelines or regression testing:**Use`tool_trajectory_avg_score`

and`response_match_score`

. These criteria are fast, predictable, and suitable for frequent automated checks.**Evaluate trusted reference responses:**Use`final_response_match_v2`

to evaluate semantic equivalence. This LLM-based check is more flexible than exact matching and better captures whether the agent's response means the same thing as the reference response.**Evaluate response quality without a reference response:**Use`rubric_based_final_response_quality_v1`

. This is useful when you don't have a trusted reference, but you can define attributes of a good response (e.g., "The response is concise," "The response has a helpful tone").**Evaluate the correctness of tool usage:**Use`rubric_based_tool_use_quality_v1`

. This allows you to validate the agent's reasoning process by checking, for example, that a specific tool was called or that tools were called in the correct order (e.g., "Tool A must be called before Tool B").**Check if responses are grounded in context:**Use`hallucinations_v1`

to detect if the agent makes claims that are unsupported by or contradictory to the information available to it (e.g., tool outputs).**Check for harmful content:**Use`safety_v1`

to ensure that agent responses are safe and do not violate safety policies.

In addition, criteria which require information on expected agent tool use
and/or responses are not supported in combination with
[User Simulation](user-sim/).
Currently, only the `hallucinations_v1`

and `safety_v1`

criteria support such evals.

### User Simulation[¶](#user-simulation)

When evaluating conversational agents, it is not always practical to use a fixed
set of user prompts, as the conversation can proceed in unexpected ways.
For example, if the agent needs the user to supply two values to perform a task,
it may ask for those values one at a time or both at once.
To resolve this issue, ADK allows you test the behavior of the agent in a
specific *conversation scenario* with user prompts that are dynamically
generated by an AI model.
For details on how to set up an eval with user simulation, see
[User Simulation](user-sim/).

## How to run Evaluation with the ADK[¶](#how-to-run-evaluation-with-the-adk)

As a developer, you can evaluate your agents using the ADK in the following ways:

**Web-based UI (**`adk web`

**):**Evaluate agents interactively through a web-based interface.**Programmatically (**`pytest`

**)**: Integrate evaluation into your testing pipeline using`pytest`

and test files.**Command Line Interface (**`adk eval`

**):**Run evaluations on an existing evaluation set file directly from the command line.

### 1. `adk web`

- Run Evaluations via the Web UI[¶](#1-adk-web-run-evaluations-via-the-web-ui)

The web UI provides an interactive way to evaluate agents, generate evaluation datasets, and inspect agent behavior in detail.

#### Step 1: Create and Save a Test Case[¶](#step-1-create-and-save-a-test-case)

- Start the web server by running:
`adk web <path_to_your_agents_folder>`

- In the web interface, select an agent and interact with it to create a session.
- Navigate to the
**Eval**tab on the right side of the interface. - Create a new eval set or select an existing one.
- Click
**"Add current session"**to save the conversation as a new evaluation case.

#### Step 2: View and Edit Your Test Case[¶](#step-2-view-and-edit-your-test-case)

Once a case is saved, you can click its ID in the list to inspect it. To make changes, click the **Edit current eval case** icon (pencil). This interactive view allows you to:

**Modify**agent text responses to refine test scenarios.**Delete**individual agent messages from the conversation.**Delete**the entire evaluation case if it's no longer needed.

#### Step 3: Run the Evaluation with Custom Metrics[¶](#step-3-run-the-evaluation-with-custom-metrics)

- Select one or more test cases from your evalset.
- Click
**Run Evaluation**. An**EVALUATION METRIC**dialog will appear. - In the dialog, use the sliders to configure the thresholds for:
**Tool trajectory avg score****Response match score**

- Click
**Start**to run the evaluation using your custom criteria. The evaluation history will record the metrics used for each run.

#### Step 4: Analyze Results[¶](#step-4-analyze-results)

After the run completes, you can analyze the results:

**Analyze Run Failures**: Click on any**Pass**or**Fail**result. For failures, you can hover over the`Fail`

label to see a side-by-side comparison of the**Actual vs. Expected Output**and the scores that caused the failure.

### Debugging with the Trace View[¶](#debugging-with-the-trace-view)

The ADK web UI includes a powerful **Trace** tab for debugging agent behavior. This feature is available for any agent session, not just during evaluation.

The **Trace** tab provides a detailed and interactive way to inspect your agent's execution flow. Traces are automatically grouped by user message, making it easy to follow the chain of events.

Each trace row is interactive:

**Hovering**over a trace row highlights the corresponding message in the chat window.**Clicking**on a trace row opens a detailed inspection panel with four tabs:**Event**: The raw event data.**Request**: The request sent to the model.**Response**: The response received from the model.**Graph**: A visual representation of the tool calls and agent logic flow.


Blue rows in the trace view indicate that an event was generated from that interaction. Clicking on these blue rows will open the bottom event detail panel, providing deeper insights into the agent's execution flow.

### 2. `pytest`

- Run Tests Programmatically[¶](#2-pytest-run-tests-programmatically)

You can also use ** pytest** to run test files as part of your integration tests.

#### Example Command[¶](#example-command)

#### Example Test Code[¶](#example-test-code)

Here is an example of a `pytest`

test case that runs a single test file:

from google.adk.evaluation.agent_evaluator import AgentEvaluator
import pytest
@pytest.mark.asyncio
async def test_with_single_test_file():
"""Test the agent's basic ability via a session file."""
await AgentEvaluator.evaluate(
agent_module="home_automation_agent",
eval_dataset_file_path_or_dir="tests/integration/fixture/home_automation_agent/simple_test.test.json",
)


This approach allows you to integrate agent evaluations into your CI/CD pipelines or larger test suites. If you want to specify the initial session state for your tests, you can do that by storing the session details in a file and passing that to `AgentEvaluator.evaluate`

method.

### 3. `adk eval`

- Run Evaluations via the CLI[¶](#3-adk-eval-run-evaluations-via-the-cli)

You can also run evaluation of an eval set file through the command line interface (CLI). This runs the same evaluation that runs on the UI, but it helps with automation, i.e. you can add this command as a part of your regular build generation and verification process.

Here is the command:

adk eval \
<AGENT_MODULE_FILE_PATH> \
<EVAL_SET_FILE_PATH> \
[--config_file_path=<PATH_TO_TEST_JSON_CONFIG_FILE>] \
[--print_detailed_results]


For example:

adk eval \
samples_for_testing/hello_world \
samples_for_testing/hello_world/hello_world_eval_set_001.evalset.json


Here are the details for each command line argument:

`AGENT_MODULE_FILE_PATH`

: The path to the`__init__.py`

file that contains a module by the name "agent". "agent" module contains a`root_agent`

.`EVAL_SET_FILE_PATH`

: The path to evaluations file(s). You can specify one or more eval set file paths. For each file, all evals will be run by default. If you want to run only specific evals from a eval set, first create a comma separated list of eval names and then add that as a suffix to the eval set file name, demarcated by a colon`:`

.- For example:
`sample_eval_set_file.json:eval_1,eval_2,eval_3`


`This will only run eval_1, eval_2 and eval_3 from sample_eval_set_file.json`

`CONFIG_FILE_PATH`

: The path to the config file.`PRINT_DETAILED_RESULTS`

: Prints detailed results on the console.
