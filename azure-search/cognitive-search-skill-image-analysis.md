---
source_url: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-image-analysis
fetched_at: 2026-01-25T03:14:52.182746
---

# Image Analysis cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Image Analysis** skill extracts a rich set of visual features based on the image content. For example, you can generate a caption from an image, generate tags, or identify celebrities and landmarks. This article is the reference documentation for the **Image Analysis** skill. See [Extract text and information from images](cognitive-search-concept-image-scenarios) for usage instructions.

This skill uses the machine learning models provided by [Azure Vision in Foundry Tools](/en-us/azure/ai-services/computer-vision/overview). **Image Analysis** works on images that meet the following requirements:

- The image must be presented in JPEG, PNG, GIF or BMP format
- The file size of the image must be less than 4 megabytes (MB)
- The dimensions of the image must be greater than 50 x 50 pixels

Supported data sources for OCR and image analysis are blobs in Azure Blob Storage and Azure Data Lake Storage (ADLS) Gen2, and image content in Microsoft OneLake. Images can be standalone files or embedded images in a PDF or other files.

This skill is implemented using the [AI Image Analysis API](/en-us/azure/ai-services/computer-vision/overview-image-analysis) version 3.2. If your solution requires calling a newer version of that service API (such as version 4.0), consider implementing through [Web API custom skill](cognitive-search-custom-skill-web-api) or use the [ImageAnalysisV4 power skill](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/Vision/ImageAnalysisV4/README.md).

Note

This skill is bound to Foundry Tools and requires [a billable resource](cognitive-search-attach-cognitive-services) for transactions that exceed 20 documents per indexer per day. Execution of built-in skills is charged at the existing [Foundry Tools Standard price](https://azure.microsoft.com/pricing/details/cognitive-services/).

In addition, image extraction is [billable by Azure AI Search](https://azure.microsoft.com/pricing/details/search/).

## @odata.type

Microsoft.Skills.Vision.ImageAnalysisSkill

## Skill parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`defaultLanguageCode` |
A string indicating the language to return. The service returns recognition results in a specified language. If this parameter isn't specified, the default value is "en". Supported languages include a subset of
|
`visualFeatures` |
An array of strings indicating the visual feature types to return. Valid visual feature types include:
color and imageType visual features have been deprecated, but you can access this functionality through a
`defaultLanguageCode` . |
`details` |
An array of strings indicating which domain-specific details to return. Valid visual feature types include:
|

## Skill inputs

| Input name | Description |
|---|---|
`image` |
Complex Type. Currently only works with "/document/normalized_images" field, produced by the Azure blob indexer when `imageAction` is set to a value other than `none` . |

## Skill outputs

| Output name | Description |
|---|---|
`adult` |
Output is a single
`isAdultContent` , `isGoryContent` , `isRacyContent` ) and double type scores (`adultScore` , `goreScore` , `racyScore` ). |

`brands`

[brand](/en-us/azure/ai-services/computer-vision/concept-brand-detection)objects, where the object is a complex type consisting of`name`

(string) and a `confidence`

score (double). It also returns a `rectangle`

with four bounding box coordinates (`x`

, `y`

, `w`

, `h`

, in pixels) indicating placement inside the image. For the rectangle, `x`

and `y`

are the top left. Bottom left is `x`

, `y+h`

. Top right is `x+w`

, `y`

. Bottom right is `x+w`

, `y+h`

.`categories`

[category](/en-us/azure/ai-services/computer-vision/concept-categorizing-images)objects, where each category object is a complex type consisting of a`name`

(string), `score`

(double), and optional `detail`

that contains celebrity or landmark details. See the [category taxonomy](/en-us/azure/ai-services/computer-vision/category-taxonomy)for the full list of category names. A detail is a nested complex type. A celebrity detail consists of a name, confidence score, and face bounding box. A landmark detail consists of a name and confidence score.`description`

[description](/en-us/azure/ai-services/computer-vision/concept-describing-images)object of a complex type, consisting of lists of`tags`

and `caption`

(an array consisting of `Text`

(string) and `confidence`

(double)).`faces`

`age`

, `gender`

, and `faceBoundingBox`

having four bounding box coordinates (in pixels) indicating placement inside the image. Coordinates are `top`

, `left`

, `width`

, `height`

.`objects`

[visual feature objects](/en-us/azure/ai-services/computer-vision/concept-object-detection). Each object is a complex type, consisting of`object`

(string), `confidence`

(double), `rectangle`

(with four bounding box coordinates indicating placement inside the image), and a `parent`

that contains an object name and confidence .`tags`

[imageTag](/en-us/azure/ai-services/computer-vision/concept-detecting-image-types)objects, where a tag object is a complex type consisting of`name`

(string), `hint`

(string), and `confidence`

(double). The addition of a hint is rare. It's only generated if a tag is ambiguous. For example, an image tagged as "curling" might have a hint of "sports" to better indicate its content.## Sample skill definition

```
{
"description": "Extract image analysis.",
"@odata.type": "#Microsoft.Skills.Vision.ImageAnalysisSkill",
"context": "/document/normalized_images/*",
"defaultLanguageCode": "en",
"visualFeatures": [
"adult",
"brands",
"categories",
"description",
"faces",
"objects",
"tags"
],
"inputs": [
{
"name": "image",
"source": "/document/normalized_images/*"
}
],
"outputs": [
{
"name": "adult"
},
{
"name": "brands"
},
{
"name": "categories"
},
{
"name": "description"
},
{
"name": "faces"
},
{
"name": "objects"
},
{
"name": "tags"
}
]
}
```


### Sample index

For single objects (such as `adult`

and `description`

), you can structure them in the index as a `Collection(Edm.ComplexType)`

to return `adult`

and `description`

output for all of them. For more information about mapping outputs to index fields, see [Flattening information from complex types](cognitive-search-output-field-mapping#flattening-information-from-complex-types).

```
{
"fields": [
{
"name": "metadata_storage_name",
"type": "Edm.String",
"key": true,
"searchable": true,
"filterable": false,
"facetable": false,
"sortable": true
},
{
"name": "metadata_storage_path",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false,
"sortable": true
},
{
"name": "content",
"type": "Edm.String",
"sortable": false,
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "adult",
"type": "Edm.ComplexType",
"fields": [
{
"name": "isAdultContent",
"type": "Edm.Boolean",
"searchable": false,
"filterable": true,
"facetable": true
},
{
"name": "isGoryContent",
"type": "Edm.Boolean",
"searchable": false,
"filterable": true,
"facetable": true
},
{
"name": "isRacyContent",
"type": "Edm.Boolean",
"searchable": false,
"filterable": true,
"facetable": true
},
{
"name": "adultScore",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "goreScore",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "racyScore",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
}
]
},
{
"name": "brands",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "name",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "rectangle",
"type": "Edm.ComplexType",
"fields": [
{
"name": "x",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "y",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "w",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "h",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
}
]
}
]
},
{
"name": "categories",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "name",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "score",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "detail",
"type": "Edm.ComplexType",
"fields": [
{
"name": "celebrities",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "name",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "faceBoundingBox",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "x",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "y",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
}
]
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
}
]
},
{
"name": "landmarks",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "name",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
}
]
}
]
}
]
},
{
"name": "description",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "tags",
"type": "Collection(Edm.String)",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "captions",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "text",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
}
]
}
]
},
{
"name": "faces",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "age",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "gender",
"type": "Edm.String",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "faceBoundingBox",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "top",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "left",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "width",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "height",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
}
]
}
]
},
{
"name": "objects",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "object",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "rectangle",
"type": "Edm.ComplexType",
"fields": [
{
"name": "x",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "y",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "w",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
},
{
"name": "h",
"type": "Edm.Int32",
"searchable": false,
"filterable": false,
"facetable": false
}
]
},
{
"name": "parent",
"type": "Edm.ComplexType",
"fields": [
{
"name": "object",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
}
]
}
]
},
{
"name": "tags",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "name",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "hint",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"facetable": false
},
{
"name": "confidence",
"type": "Edm.Double",
"searchable": false,
"filterable": false,
"facetable": false
}
]
}
]
}
```


### Sample output field mapping

The target field can be a complex field or collection. The index definition specifies any subfields.

```
"outputFieldMappings": [
{
"sourceFieldName": "/document/normalized_images/*/adult",
"targetFieldName": "adult"
},
{
"sourceFieldName": "/document/normalized_images/*/brands/*",
"targetFieldName": "brands"
},
{
"sourceFieldName": "/document/normalized_images/*/categories/*",
"targetFieldName": "categories"
},
{
"sourceFieldName": "/document/normalized_images/*/description",
"targetFieldName": "description"
},
{
"sourceFieldName": "/document/normalized_images/*/faces/*",
"targetFieldName": "faces"
},
{
"sourceFieldName": "/document/normalized_images/*/objects/*",
"targetFieldName": "objects"
},
{
"sourceFieldName": "/document/normalized_images/*/tags/*",
"targetFieldName": "tags"
}
```


### Variation on output field mappings (nested properties)

You can define output field mappings to lower-level properties, such as just celebrities or landmarks. In this case, make sure your index schema has a field to contain each detail specifically.

```
"outputFieldMappings": [
{
"sourceFieldName": "/document/normalized_images/*/categories/detail/celebrities/*",
"targetFieldName": "celebrities"
},
{
"sourceFieldName": "/document/normalized_images/*/categories/detail/landmarks/*",
"targetFieldName": "landmarks"
}
```


## Sample input

```
{
"values": [
{
"recordId": "1",
"data": {
"image": {
"data": "BASE64 ENCODED STRING OF A JPEG IMAGE",
"width": 500,
"height": 300,
"originalWidth": 5000,
"originalHeight": 3000,
"rotationFromOriginal": 90,
"contentOffset": 500,
"pageNumber": 2
}
}
}
]
}
```


## Sample output

```
{
"values": [
{
"recordId": "1",
"data": {
"categories": [
{
"name": "abstract_",
"score": 0.00390625
},
{
"name": "people_",
"score": 0.83984375,
"detail": {
"celebrities": [
{
"name": "Satya Nadella",
"faceBoundingBox": [
{
"x": 273,
"y": 309
},
{
"x": 395,
"y": 309
},
{
"x": 395,
"y": 431
},
{
"x": 273,
"y": 431
}
],
"confidence": 0.999028444
}
],
"landmarks": [ ]
}
}
],
"adult": {
"isAdultContent": false,
"isRacyContent": false,
"isGoryContent": false,
"adultScore": 0.0934349000453949,
"racyScore": 0.068613491952419281,
"goreScore": 0.08928389008070282
},
"tags": [
{
"name": "person",
"confidence": 0.98979085683822632
},
{
"name": "man",
"confidence": 0.94493889808654785
},
{
"name": "outdoor",
"confidence": 0.938492476940155
},
{
"name": "window",
"confidence": 0.89513939619064331
}
],
"description": {
"tags": [
"person",
"man",
"outdoor",
"window",
"glasses"
],
"captions": [
{
"text": "Satya Nadella sitting on a bench",
"confidence": 0.48293603002174407
}
]
},
"faces": [
{
"age": 44,
"gender": "Male",
"faceBoundingBox": [
{
"x": 1601,
"y": 395
},
{
"x": 1653,
"y": 395
},
{
"x": 1653,
"y": 447
},
{
"x": 1601,
"y": 447
}
]
}
],
"objects": [
{
"rectangle": {
"x": 25,
"y": 43,
"w": 172,
"h": 140
},
"object": "person",
"confidence": 0.931
}
],
"brands":[
{
"name":"Microsoft",
"confidence": 0.903,
"rectangle":{
"x":20,
"y":97,
"w":62,
"h":52
}
}
]
}
}
]
}
```


## Error cases

In the following error cases, no elements are extracted.

| Error Code | Description |
|---|---|
`NotSupportedLanguage` |
The language provided isn't supported. |
`InvalidImageUrl` |
Image URL is badly formatted or not accessible. |
`InvalidImageFormat` |
Input data isn't a valid image. |
`InvalidImageSize` |
Input image is too large. |
`NotSupportedVisualFeature` |
Specified feature type isn't valid. |
`NotSupportedImage` |
Unsupported image, for example, child pornography. |
`InvalidDetails` |
Unsupported domain-specific model. |

If you get the error similar to `"One or more skills are invalid. Details: Error in skill #<num>: Outputs are not supported by skill: Landmarks"`

, check the path. Both celebrities and landmarks are properties under `detail`

.

```
"categories":[
{
"name":"building_",
"score":0.97265625,
"detail":{
"landmarks":[
{
"name":"Forbidden City",
"confidence":0.92013400793075562
}
]
```