---
merged_at: 2026-01-25T15:38:56.564718
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___googlecloudbigqueryjobschemaupdateoption_googlecloudbigqueryenumsschemaupdate_2dc958.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigqueryjobschemaupdateoption_googlecloudbigqueryenumsschemaupdateo_174e49.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryjobschemaupdateoption_googlecloudbigqueryenumsschemaupdateop_9d5aba.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryjobschemaupdateoption.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.job.SchemaUpdateOption -->

# Class SchemaUpdateOption (3.40.0)

`SchemaUpdateOption()`


Specifies an update to the destination table schema as a side effect of a load job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsschemaupdateoption.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SchemaUpdateOption -->

# Class SchemaUpdateOption (3.40.0)

`SchemaUpdateOption()`


Specifies an update to the destination table schema as a side effect of a load job.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquerymodeltransformcolumn.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.model.TransformColumn -->

# Class TransformColumn (3.40.0)

`TransformColumn(resource: typing.Dict[str, typing.Any])`


TransformColumn represents a transform column feature.

See
[https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn](https://cloud.google.com/bigquery/docs/reference/rest/v2/models#transformcolumn)

## Properties

### name

Name of the column.

### transform_sql

The SQL expression used in the column transform.

### type_

Data type of the column after the transform.

Returns |
|
|---|---|
Type |
Description |
`Optional[` |
Data type of the column. |

## Methods

### from_api_repr

```
from_api_repr(
resource: typing.Dict[str, typing.Any],
) -> google.cloud.bigquery.model.TransformColumn
```


Constructs a transform column feature given its API representation


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryrangequeryparameter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.RangeQueryParameter -->

# Class RangeQueryParameter (3.40.0)

`RangeQueryParameter(range_element_type, start=None, end=None, name=None)`


Named / positional query parameters for range values.

## Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of 'TIMESTAMP', 'DATE', or 'DATETIME'. |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`name` |
`Optional[str]`
Parameter name, used via |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.RangeQueryParameter`


Factory: construct parameter from JSON resource.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict`
JSON mapping of parameter |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameter` |
Instance |

### positional

```
positional(
range_element_type, start=None, end=None
) -> google.cloud.bigquery.query.RangeQueryParameter
```


Factory for positional parameters.

Parameters |
|
|---|---|
Name |
Description |
`range_element_type` |
`Union[str, RangeQueryParameterType]`
The type of range elements. It must be one of |
`start` |
`Optional[Union[ScalarQueryParameter, str]]`
The start of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |
`end` |
`Optional[Union[ScalarQueryParameter, str]]`
The end of the range value. Must be the same type as range_element_type. If not provided, it's interpreted as UNBOUNDED. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.RangeQueryParameter` |
Instance without name. |

### to_api_repr

`to_api_repr() -> dict`


Construct JSON API representation for the parameter.

Returns |
|
|---|---|
Type |
Description |
`Dict` |
JSON mapping |


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryroutineroutinereference___googlecloudbigquery_v2typesmodelho_df3a27.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryroutineroutinereference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.routine.RoutineReference -->

# Class RoutineReference (3.40.0)

`RoutineReference()`


A pointer to a routine.

See:
[https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference](https://cloud.google.com/bigquery/docs/reference/rest/v2/routines#routinereference)

## Properties

### dataset_id

str: ID of dataset containing the routine.

### path

str: URL path for the routine's APIs.

### project

str: ID of the project containing the routine.

### routine_id

str: The routine ID.

## Methods

### __eq__

`__eq__(other)`


Two RoutineReferences are equal if they point to the same routine.

### __str__

`__str__()`


String representation of the reference.

This is a fully-qualified ID, including the project ID and dataset ID.

### from_api_repr

```
from_api_repr(
resource: dict,
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference given its API representation.

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
Routine reference representation returned from the API. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `resource` . |

### from_string

```
from_string(
routine_id: str, default_project: typing.Optional[str] = None
) -> google.cloud.bigquery.routine.routine.RoutineReference
```


Factory: construct a routine reference from routine ID string.

Parameters |
|
|---|---|
Name |
Description |
`routine_id` |
`str`
A routine ID in standard SQL format. If |
`default_project` |
`Optional[str]`
The project ID to use when |

Exceptions |
|
|---|---|
Type |
Description |
`ValueError` |
If `routine_id` is not a fully-qualified routine ID in standard SQL format. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.routine.RoutineReference` |
Routine reference parsed from `routine_id` . |

### to_api_repr

`to_api_repr() -> dict`


Construct the API resource representation of this routine reference.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Routine reference represented as an API resource. |


---

<!-- DOCUMENTO FUSIONADO: __googlecloudbigquery_v2typesmodelholidayregion_googlecloudbigquery_v2typesmodel_eb19e0.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesmodelholidayregion_googlecloudbigquery_v2typesmodell_534858.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelholidayregion.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.HolidayRegion -->

# Class HolidayRegion (3.40.0)

`HolidayRegion(value)`


Type of supported holiday regions for time series forecasting models.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodellearnratestrategy.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.LearnRateStrategy -->

# Class LearnRateStrategy (3.40.0)

`LearnRateStrategy(value)`


Indicates the learning rate optimization strategy to use.


---

<!-- DOCUMENTO FUSIONADO: _summary_overview_googlecloudbigqueryenumsstandardsqltypenames.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: summary_overview.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/summary_overview -->

# Google Cloud BigQuery API

Overview of the APIs available for Google Cloud BigQuery API.

## All entries

Classes, methods and properties & attributes for Google Cloud BigQuery API.


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumsstandardsqltypenames.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.StandardSqlTypeNames -->

# Class StandardSqlTypeNames (3.40.0)

`StandardSqlTypeNames(value)`


Enum of allowed SQL type names in schema.SchemaField.

Datatype used in GoogleSQL.
