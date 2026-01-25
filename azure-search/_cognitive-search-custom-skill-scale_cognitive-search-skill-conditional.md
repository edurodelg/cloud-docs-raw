---
merged_at: 2026-01-25T03:18:13.769617
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-custom-skill-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-custom-skill-scale -->

# Efficiently scale out a custom skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Custom skills are web APIs that implement a specific interface. A custom skill can be implemented on any publicly addressable resource. The most common implementations for custom skills are:

- Azure Functions for custom logic skills
- Azure Web apps for simple containerized AI skills
- Azure Kubernetes service for more complex or larger skills.

## Skillset configuration

The following properties on a [custom skill](cognitive-search-custom-skill-web-api) are used for scale. Review the [custom skill interface](cognitive-search-custom-skill-interface) for an introduction into the inputs and outputs that a custom skill should implement.

Set

`batchSize`

of the custom skill to configure the number of records sent to the skill in a single invocation of the skill.Set the

`degreeOfParallelism`

to calibrate the number of concurrent requests the indexer makes to your skill.Set

`timeout`

to a value sufficient for the skill to respond with a valid response.In the

`indexer`

definition, setto the number of documents that should be read from the data source and enriched concurrently.`batchSize`


### Considerations

There's no "one size fits all" set of recommendations. You should plan on testing different configurations to reach an optimum result. Scale up strategies are based on fewer large requests, or many small requests.

Skill invocation cardinality: make sure you know whether the custom skill executes once for each document (

`/document/content`

) or multiple times per document (`/document/reviews_text/pages/*`

). If it's multiple times per document, stay on the lower side of`batchSize`

and`degreeOfParallelism`

to reduce churn, and try setting indexer batch size to incrementally higher values for more scale.Coordinate custom skill

`batchSize`

and indexer`batchSize`

, and make sure you're not creating bottlenecks. For example, if the indexer batch size is 5, and the skill batch size is 50, you would need 10 indexer batches to fill a custom skill request. Ideally, skill batch size should be less than or equal to indexer batch size.For

`degreeOfParallelism`

, use the average number of requests an indexer batch can generate to guide your decision on how to set this value. If your infrastructure hosting the skill, for example an Azure function, can't support high levels of concurrency, consider dialing down the degrees of parallelism. You can test your configuration with a few documents to validate your understanding of average number of requests.Although your object is scale and support of high volumes, testing with a smaller sample of documents helps quantify different stages of execution. For example, you can evaluate the execution time of your skill, relative to the overall time taken to process the subset of documents. This helps you answer the question: does your indexer spend more time building a batch or waiting for a response from your skill?

Consider the upstream implications of parallelism. If the input to a custom skill is an output from a prior skill, are all the skills in the skillset scaled out effectively to minimize latency?


## Error handling in the custom skill

Custom skills should return a success status code HTTP 200 when the skill completes successfully. If one or more records in a batch result in errors, consider returning multi-status code 207. The errors or warnings list for the record should contain the appropriate message.

Any items in a batch that errors will result in the corresponding document failing. If you need the document to succeed, return a warning.

Any status code over 299 is evaluated as an error and all the enrichments are failed resulting in a failed document.

### Common error messages

`Could not execute skill because it did not execute within the time limit '00:00:30'. This is likely transient. Please try again later. For custom skills, consider increasing the 'timeout' parameter on your skill in the skillset.`

Set the timeout parameter on the skill to allow for a longer execution duration.`Could not execute skill because Web Api skill response is invalid.`

Indicative of the skill not returning a message in the custom skill response format. This could be the result of an uncaught exception in the skill.`Could not execute skill because the Web Api request failed.`

Most likely caused by authorization errors or exceptions.`Could not execute skill.`

Commonly the result of the skill response being mapped to an existing property in the document hierarchy.

## Testing custom skills

Start by testing your custom skill with a REST API client to validate:

The skill implements the custom skill interface for requests and responses

The skill returns valid JSON with the

`application/JSON`

MIME typeReturns a valid HTTP status code


Create a [debug session](cognitive-search-debug-session) to add your skill to the skillset and make sure it produces a valid enrichment. While a debug session doesn't allow you to tune the performance of the skill, it enables you to ensure that the skill is configured with valid values and returns the expected enriched objects.

## Best practices

While skills can accept and return larger payloads, consider limiting the response to 150 MB or less when returning JSON.

Consider setting the batch size on the indexer and skill to ensure that each data source batch generates a full payload for your skill.

For long running tasks, set the timeout to a high enough value to ensure the indexer doesn't error out when processing documents concurrently.

Optimize the indexer batch size, skill batch size, and skill degrees of parallelism to generate the load pattern your skill expects, fewer large requests or many small requests.

Monitor custom skills with detailed logs of failures as you can have scenarios where specific requests consistently fail as a result of the data variability.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-conditional.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-conditional -->

# Conditional cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Conditional** skill enables Azure AI Search scenarios that require a Boolean operation to determine the data to assign to an output. These scenarios include filtering, assigning a default value, and merging data based on a condition.

The following pseudocode demonstrates what the conditional skill accomplishes:

```
if (condition)
{ output = whenTrue }
else
{ output = whenFalse }
```


Note

This skill isn't bound to Foundry Tools. It's nonbillable and has no Foundry Tools key requirement.

## @odata.type

Microsoft.Skills.Util.ConditionalSkill

## Evaluated fields

This skill is special because its inputs are evaluated fields.

The following items are valid values of an expression:

Annotation paths (paths in expressions must be delimited by "$(" and ")")


Examples:`"= $(/document)" "= $(/document/content)"`

Literals (strings, numbers, true, false, null)


Examples:`"= 'this is a string'" // string (note the single quotation marks) "= 34" // number "= true" // Boolean "= null" // null value`

Expressions that use comparison operators (==, !=, >=, >, <=, <)


Examples:`"= $(/document/language) == 'en'" "= $(/document/sentiment) >= 0.5"`

Expressions that use Boolean operators (&&, ||, !, ^)


Examples:`"= $(/document/language) == 'en' && $(/document/sentiment) > 0.5" "= !true"`

Expressions that use numeric operators (+, -, *, /, %)


Examples:`"= $(/document/sentiment) + 0.5" // addition "= $(/document/totalValue) * 1.10" // multiplication "= $(/document/lengthInMeters) / 0.3049" // division`


Because the conditional skill supports evaluation, you can use it in minor-transformation scenarios. For example, see [skill definition 4](#transformation-example).

## Skill inputs

Inputs are case-sensitive.

| Input | Description |
|---|---|
| condition | This input is an
true or false). Examples: "= true" "= $(/document/language) =='fr'" "= $(/document/pages/*/language) == $(/document/expectedLanguage)" |

[evaluated field](#evaluated-fields)that represents the value to return if the condition is evaluated to*true*. Constants strings should be returned in single quotation marks (' and ').Sample values:

"= 'contract'"

"= $(/document/contractType)"

"= $(/document/entities/*)"

[evaluated field](#evaluated-fields)that represents the value to return if the condition is evaluated to*false*.Sample values:

"= 'contract'"

"= $(/document/contractType)"

"= $(/document/entities/*)"

## Skill outputs

There's a single output called "output." It returns the value *whenFalse* if the condition is false or *whenTrue* if the condition is true.

## Examples

### Sample skill definition 1: Filter documents to return only French documents

The following output returns an array of sentences ("/document/frenchSentences") if the language of the document is French. If the language isn't French, the value is set to *null*.

```
{
"@odata.type": "#Microsoft.Skills.Util.ConditionalSkill",
"context": "/document",
"inputs": [
{ "name": "condition", "source": "= $(/document/language) == 'fr'" },
{ "name": "whenTrue", "source": "/document/sentences" },
{ "name": "whenFalse", "source": "= null" }
],
"outputs": [ { "name": "output", "targetName": "frenchSentences" } ]
}
```


If "/document/frenchSentences" is used as the *context* of another skill, that skill only runs if "/document/frenchSentences" isn't set to *null*.

### Sample skill definition 2: Set a default value for a value that doesn't exist

The following output creates an annotation ("/document/languageWithDefault") that set to the language of the document or to "es" if the language isn't set.

```
{
"@odata.type": "#Microsoft.Skills.Util.ConditionalSkill",
"context": "/document",
"inputs": [
{ "name": "condition", "source": "= $(/document/language) == null" },
{ "name": "whenTrue", "source": "= 'es'" },
{ "name": "whenFalse", "source": "= $(/document/language)" }
],
"outputs": [ { "name": "output", "targetName": "languageWithDefault" } ]
}
```


### Sample skill definition 3: Merge values from two fields into one

In this example, some sentences have a *frenchSentiment* property. Whenever the *frenchSentiment* property is null, we want to use the *englishSentiment* value. We assign the output to a member called *sentiment* ("/document/sentences/*/sentiment").

```
{
"@odata.type": "#Microsoft.Skills.Util.ConditionalSkill",
"context": "/document/sentences/*",
"inputs": [
{ "name": "condition", "source": "= $(/document/sentences/*/frenchSentiment) == null" },
{ "name": "whenTrue", "source": "/document/sentences/*/englishSentiment" },
{ "name": "whenFalse", "source": "/document/sentences/*/frenchSentiment" }
],
"outputs": [ { "name": "output", "targetName": "sentiment" } ]
}
```


## Transformation example

### Sample skill definition 4: Data transformation on a single field

In this example, we receive a *sentiment* that's between 0 and 1. We want to transform it to be between -1 and 1. We can use the conditional skill to do this minor transformation.

In this example, we don't use the conditional aspect of the skill because the condition is always *true*.

```
{
"@odata.type": "#Microsoft.Skills.Util.ConditionalSkill",
"context": "/document/sentences/*",
"inputs": [
{ "name": "condition", "source": "= true" },
{ "name": "whenTrue", "source": "= $(/document/sentences/*/sentiment) * 2 - 1" },
{ "name": "whenFalse", "source": "= 0" }
],
"outputs": [ { "name": "output", "targetName": "normalizedSentiment" } ]
}
```


## Special considerations

Some parameters are evaluated, so you need to be especially careful to follow the documented pattern. Expressions must start with an equals sign. A path must be delimited by "$(" and ")". Make sure to put strings in single quotation marks. That helps the evaluator distinguish between strings and actual paths and operators. Also, make sure to put white space around operators (for instance, a "*" in a path means something different than multiply).
