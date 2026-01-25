---
merged_at: 2026-01-25T15:38:56.572450
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _index_reference.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest -->

# Python Client for Google BigQuery

Querying massive datasets can be time consuming and expensive without the
right hardware and infrastructure. Google [BigQuery](https://cloud.google.com/bigquery/what-is-bigquery) solves this problem by
enabling super-fast, SQL queries against append-mostly tables, using the
processing power of Google’s infrastructure.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Supported Python Versions

Python >= 3.9

#### Unsupported Python Versions

Python == 2.7, Python == 3.5, Python == 3.6, Python == 3.7, and Python == 3.8.

The last version of this library compatible with Python 2.7 and 3.5 is google-cloud-bigquery==1.28.0.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-bigquery
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-bigquery
```


## Example Usage

### Perform a query

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
# Perform a query.
QUERY = (
'SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` '
'WHERE state = "TX" '
'LIMIT 100')
query_job = client.[query](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)(QUERY) # API request
rows = [query_job](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor.html#google_cloud_bigquery_dbapi_Cursor_query_job).result() # Waits for query to finish
for row in rows:
print(row.name)


## Instrumenting With OpenTelemetry

This application uses [OpenTelemetry](https://opentelemetry.io) to output tracing data from
API calls to BigQuery. To enable OpenTelemetry tracing in
the BigQuery client the following PyPI packages need to be installed:

```
pip install google-cloud-bigquery[opentelemetry] opentelemetry-exporter-gcp-trace
```


After installation, OpenTelemetry can be used in the BigQuery client and in BigQuery jobs. First, however, an exporter must be specified for where the trace data will be outputted to. An example of this can be found here:

```
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.cloud_trace import CloudTraceSpanExporter
tracer_provider = TracerProvider()
tracer_provider = BatchSpanProcessor(CloudTraceSpanExporter())
trace.set_tracer_provider(TracerProvider())
```


In this example all tracing data will be published to the Google
[Cloud Trace](https://cloud.google.com/trace) console. For more information on OpenTelemetry, please consult the [OpenTelemetry documentation](https://opentelemetry-python.readthedocs.io).


---

<!-- DOCUMENTO FUSIONADO: reference.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/reference -->

# Python Client for Google BigQuery

Querying massive datasets can be time consuming and expensive without the
right hardware and infrastructure. Google [BigQuery](https://cloud.google.com/bigquery/what-is-bigquery) solves this problem by
enabling super-fast, SQL queries against append-mostly tables, using the
processing power of Google’s infrastructure.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Supported Python Versions

Python >= 3.9

#### Unsupported Python Versions

Python == 2.7, Python == 3.5, Python == 3.6, Python == 3.7, and Python == 3.8.

The last version of this library compatible with Python 2.7 and 3.5 is google-cloud-bigquery==1.28.0.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-bigquery
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-bigquery
```


## Example Usage

### Perform a query

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
# Perform a query.
QUERY = (
'SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` '
'WHERE state = "TX" '
'LIMIT 100')
query_job = client.[query](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)(QUERY) # API request
rows = [query_job](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor.html#google_cloud_bigquery_dbapi_Cursor_query_job).result() # Waits for query to finish
for row in rows:
print(row.name)


## Instrumenting With OpenTelemetry

This application uses [OpenTelemetry](https://opentelemetry.io) to output tracing data from
API calls to BigQuery. To enable OpenTelemetry tracing in
the BigQuery client the following PyPI packages need to be installed:

```
pip install google-cloud-bigquery[opentelemetry] opentelemetry-exporter-gcp-trace
```


After installation, OpenTelemetry can be used in the BigQuery client and in BigQuery jobs. First, however, an exporter must be specified for where the trace data will be outputted to. An example of this can be found here:

```
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.cloud_trace import CloudTraceSpanExporter
tracer_provider = TracerProvider()
tracer_provider = BatchSpanProcessor(CloudTraceSpanExporter())
trace.set_tracer_provider(TracerProvider())
```


In this example all tracing data will be published to the Google
[Cloud Trace](https://cloud.google.com/trace) console. For more information on OpenTelemetry, please consult the [OpenTelemetry documentation](https://opentelemetry-python.readthedocs.io).


---

<!-- DOCUMENTO FUSIONADO: _standard_sql__googlecloudbigqueryqueryarrayqueryparameter__googlecloudbigquery__d27877.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: standard_sql.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/standard_sql -->

# Python Client for Google BigQuery

Querying massive datasets can be time consuming and expensive without the
right hardware and infrastructure. Google [BigQuery](https://cloud.google.com/bigquery/what-is-bigquery) solves this problem by
enabling super-fast, SQL queries against append-mostly tables, using the
processing power of Google’s infrastructure.

## Quick Start

In order to use this library, you first need to go through the following steps:

### Installation

Install this library in a [virtualenv](https://virtualenv.pypa.io/en/latest/) using pip. [virtualenv](https://virtualenv.pypa.io/en/latest/) is a tool to
create isolated Python environments. The basic problem it addresses is one of
dependencies and versions, and indirectly permissions.

With [virtualenv](https://virtualenv.pypa.io/en/latest/), it’s possible to install this library without needing system
install permissions, and without clashing with the installed system
dependencies.

#### Supported Python Versions

Python >= 3.9

#### Unsupported Python Versions

Python == 2.7, Python == 3.5, Python == 3.6, Python == 3.7, and Python == 3.8.

The last version of this library compatible with Python 2.7 and 3.5 is google-cloud-bigquery==1.28.0.

#### Mac/Linux

```
pip install virtualenv
virtualenv <your-env>
source <your-env>/bin/activate
<your-env>/bin/pip install google-cloud-bigquery
```


#### Windows

```
pip install virtualenv
virtualenv <your-env>
<your-env>\Scripts\activate
<your-env>\Scripts\pip.exe install google-cloud-bigquery
```


## Example Usage

### Perform a query

`from google.cloud import `[bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest)
client = [bigquery](https://docs.cloud.google.com/python/docs/reference/bigquery/latest).[Client](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)()
# Perform a query.
QUERY = (
'SELECT name FROM `bigquery-public-data.usa_names.usa_1910_2013` '
'WHERE state = "TX" '
'LIMIT 100')
query_job = client.[query](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.client.Client.html)(QUERY) # API request
rows = [query_job](https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.dbapi.Cursor.html#google_cloud_bigquery_dbapi_Cursor_query_job).result() # Waits for query to finish
for row in rows:
print(row.name)


## Instrumenting With OpenTelemetry

This application uses [OpenTelemetry](https://opentelemetry.io) to output tracing data from
API calls to BigQuery. To enable OpenTelemetry tracing in
the BigQuery client the following PyPI packages need to be installed:

```
pip install google-cloud-bigquery[opentelemetry] opentelemetry-exporter-gcp-trace
```


After installation, OpenTelemetry can be used in the BigQuery client and in BigQuery jobs. First, however, an exporter must be specified for where the trace data will be outputted to. An example of this can be found here:

```
from opentelemetry import trace
from opentelemetry.sdk.trace import TracerProvider
from opentelemetry.sdk.trace.export import BatchSpanProcessor
from opentelemetry.exporter.cloud_trace import CloudTraceSpanExporter
tracer_provider = TracerProvider()
tracer_provider = BatchSpanProcessor(CloudTraceSpanExporter())
trace.set_tracer_provider(TracerProvider())
```


In this example all tracing data will be published to the Google
[Cloud Trace](https://cloud.google.com/trace) console. For more information on OpenTelemetry, please consult the [OpenTelemetry documentation](https://opentelemetry-python.readthedocs.io).


---

<!-- DOCUMENTO FUSIONADO: _googlecloudbigqueryqueryarrayqueryparameter__googlecloudbigquery_v2typesstandar_23bb29.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryqueryarrayqueryparameter.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.query.ArrayQueryParameter -->

# Class ArrayQueryParameter (3.40.0)

`ArrayQueryParameter(name, array_type, values)`


Named / positional query parameters for array values.

## Parameters |
|
|---|---|
Name |
Description |
`name` |
`Optional[str]`
Parameter name, used via |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

## Methods

### from_api_repr

`from_api_repr(resource: dict) -> google.cloud.bigquery.query.ArrayQueryParameter`


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
`google.cloud.bigquery.query.ArrayQueryParameter` |
Instance |

### positional

```
positional(
array_type: str, values: list
) -> google.cloud.bigquery.query.ArrayQueryParameter
```


Factory for positional parameters.

Parameters |
|
|---|---|
Name |
Description |
`array_type` |
`Union[str, ScalarQueryParameterType, StructQueryParameterType]`
The type of array elements. If given as a string, it must be one of |
`values` |
`List[appropriate type]`
The parameter array values. |

Returns |
|
|---|---|
Type |
Description |
`google.cloud.bigquery.query.ArrayQueryParameter` |
Instance without name |

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

<!-- DOCUMENTO FUSIONADO: _googlecloudbigquery_v2typesstandardsqlstructtype_googlecloudbigquery_v2typesmod_235742.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesstandardsqlstructtype.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.StandardSqlStructType -->

# Class StandardSqlStructType (3.40.0)

[[["Easy to understand","easyToUnderstand","thumb-up"],["Solved my problem","solvedMyProblem","thumb-up"],["Other","otherUp","thumb-up"]],[["Hard to understand","hardToUnderstand","thumb-down"],["Incorrect information or sample code","incorrectInformationOrSampleCode","thumb-down"],["Missing the information/samples I need","missingTheInformationSamplesINeed","thumb-down"],["Other","otherDown","thumb-down"]],["Last updated 2026-01-09 UTC."],[],[]]


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrixentry.md -->
<!-- URL ORIGINAL: https://cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Entry -->

# Class Entry (3.40.0)

`Entry(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single entry in the confusion matrix.

## Attributes |
|
|---|---|
Name |
Description |
`predicted_label` |
`str`
The predicted label. For confidence_threshold > 0, we will also add an entry indicating the number of items under the confidence threshold. |
`item_count` |
`google.protobuf.wrappers_pb2.Int64Value`
Number of items being predicted as this label. |
