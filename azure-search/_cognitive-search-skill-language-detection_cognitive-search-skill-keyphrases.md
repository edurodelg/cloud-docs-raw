---
merged_at: 2026-01-25T03:18:13.746395
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-language-detection.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-language-detection -->

# Language detection cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Language Detection** skill detects the language of input text and reports a single language code for every document submitted on the request. The language code is paired with a score indicating the strength of the analysis. This skill uses the machine learning models provided in [Azure Language in Foundry Tools](/en-us/azure/ai-services/language-service/overview).

This capability is especially useful when you need to provide the language of the text as input to other skills (for example, the [Sentiment Analysis skill](cognitive-search-skill-sentiment-v3) or [Text Split skill](cognitive-search-skill-textsplit)).

See [supported languages](/en-us/azure/ai-services/language-service/language-detection/language-support) for Language Detection. If you have content expressed in an unsupported language, the response is `(Unknown)`

.

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## @odata.type

Microsoft.Skills.Text.LanguageDetectionSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the language detection skill, you can use the

[Text Split skill](cognitive-search-skill-textsplit).

## Skill parameters

Parameters are case sensitive.

| Inputs | Description |
|---|---|
`defaultCountryHint` |
(Optional) An ISO 3166-1 alpha-2 two letter country code can be provided to use as a hint to the language detection model if it can't
`defaultCountryHint` parameter is used with documents that don't specify the `countryHint` input explicitly. |

`modelVersion`

[version of the model](/en-us/azure/ai-services/language-service/concepts/model-lifecycle)to use when calling language detection. It defaults to the latest available when not specified. We recommend you don't specify this value unless it's necessary.## Skill inputs

Parameters are case sensitive.

| Inputs | Description |
|---|---|
`text` |
The text to be analyzed. |
`countryHint` |
An ISO 3166-1 alpha-2 two letter country code to use as a hint to the language detection model if it can't
|

## Skill outputs

| Output Name | Description |
|---|---|
`languageCode` |
The ISO 6391 language code for the language identified. For example, "en". |
`languageName` |
The name of language. For example, "English". |
`score` |
A value between 0 and 1. The likelihood that language is correctly identified. The score can be lower than 1 if the sentence has mixed languages. |

## Sample definition

```
{
"@odata.type": "#Microsoft.Skills.Text.LanguageDetectionSkill",
"inputs": [
{
"name": "text",
"source": "/document/text"
},
{
"name": "countryHint",
"source": "/document/countryHint"
}
],
"outputs": [
{
"name": "languageCode",
"targetName": "myLanguageCode"
},
{
"name": "languageName",
"targetName": "myLanguageName"
},
{
"name": "score",
"targetName": "myLanguageScore"
}
]
}
```


## Sample input

```
{
"values": [
{
"recordId": "1",
"data":
{
"text": "Glaciers are huge rivers of ice that ooze their way over land, powered by gravity and their own sheer weight. "
}
},
{
"recordId": "2",
"data":
{
"text": "Estamos muy felices de estar con ustedes."
}
},
{
"recordId": "3",
"data":
{
"text": "impossible",
"countryHint": "fr"
}
}
]
```


## Sample output

```
{
"values": [
{
"recordId": "1",
"data":
{
"languageCode": "en",
"languageName": "English",
"score": 1,
}
},
{
"recordId": "2",
"data":
{
"languageCode": "es",
"languageName": "Spanish",
"score": 1,
}
},
{
"recordId": "3",
"data":
{
"languageCode": "fr",
"languageName": "French",
"score": 1,
}
}
]
}
```


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-keyphrases.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-keyphrases -->

# Key Phrase Extraction cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Key Phrase Extraction** skill evaluates unstructured text, and for each record, returns a list of key phrases. This skill uses the [Key Phrase](/en-us/azure/ai-services/language-service/key-phrase-extraction/overview) machine learning models provided by [Azure Language in Foundry Tools](/en-us/azure/ai-services/language-service/overview).

This capability is useful if you need to quickly identify the main talking points in the record. For example, given input text "The food was delicious and there were wonderful staff", the service returns "food" and "wonderful staff".

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

## @odata.type

Microsoft.Skills.Text.KeyPhraseExtractionSkill

## Data limits

The maximum size of a record should be 50,000 characters as measured by [ String.Length](/en-us/dotnet/api/system.string.length). If you need to break up your data before sending it to the key phrase extractor, consider using the

[Text Split skill](cognitive-search-skill-textsplit). If you do use a text split skill, set the page length to 5000 for the best performance.

## Skill parameters

Parameters are case sensitive.

| Inputs | Description |
|---|---|
`defaultLanguageCode` |
(Optional) The language code to apply to documents that don't specify language explicitly. If the default language code isn't specified, English (en) is used as the default language code. See the
|
`maxKeyPhraseCount` |
(Optional) The maximum number of key phrases to produce. |
`modelVersion` |
(Optional) Specifies the
|

## Skill inputs

| Input | Description |
|---|---|
`text` |
The text to be analyzed. |
`languageCode` |
A string indicating the language of the records. If this parameter isn't specified, the default language code is used to analyze the records. See the
|

## Skill outputs

| Output | Description |
|---|---|
`keyPhrases` |
A list of key phrases extracted from the input text. The key phrases are returned in order of importance. |

## Sample definition

Consider a SQL record that has the following fields:

```
{
"content": "Glaciers are huge rivers of ice that ooze their way over land, powered by gravity and their own sheer weight. They accumulate ice from snowfall and lose it through melting. As global temperatures have risen, many of the world’s glaciers have already started to shrink and retreat. Continued warming could see many iconic landscapes – from the Canadian Rockies to the Mount Everest region of the Himalayas – lose almost all their glaciers by the end of the century.",
"language": "en"
}
```


Then your skill definition might look like this:

```
{
"@odata.type": "#Microsoft.Skills.Text.KeyPhraseExtractionSkill",
"inputs": [
{
"name": "text",
"source": "/document/content"
},
{
"name": "languageCode",
"source": "/document/language"
}
],
"outputs": [
{
"name": "keyPhrases",
"targetName": "myKeyPhrases"
}
]
}
```


## Sample output

For the previous example, the output of your skill is written to a new node in the enriched tree called "document/myKeyPhrases" since that is the `targetName`

that we specified. If you don’t specify a `targetName`

, then it would be "document/keyPhrases".

#### document/myKeyPhrases

```
[
"world’s glaciers",
"huge rivers of ice",
"Canadian Rockies",
"iconic landscapes",
"Mount Everest region",
"Continued warming"
]
```


You can use "document/myKeyPhrases" as input into other skills, or as a source of an [output field mapping](cognitive-search-output-field-mapping).

## Warnings

If you provide an unsupported language code, a warning is generated and key phrases aren't extracted. If your text is empty, a warning is produced. If your text is larger than 50,000 characters, only the first 50,000 characters are analyzed and a warning is issued.
