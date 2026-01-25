---
merged_at: 2026-01-25T02:14:48.520398
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: googlecloudbigqueryenumssourceformat.md -->
<!-- URL ORIGINAL: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.SourceFormat -->

# Class SourceFormat (3.40.0)


      
      Save and categorize content based on your preferences.

`SourceFormat()`


The format of the data files. The default value is `CSV`

.

Note that the set of allowed values for loading data is different
than the set used for external data sources (see
[ExternalSourceFormat](/python/docs/reference/bigquery/latest/google.cloud.bigquery.external_config.ExternalSourceFormat)).


---

<!-- DOCUMENTO FUSIONADO: googlecloudbigquery_v2typesmodelmulticlassclassificationmetricsconfusionmatrixrow.md -->
<!-- URL ORIGINAL: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.MultiClassClassificationMetrics.ConfusionMatrix.Row -->

# Class Row (3.40.0)


      
      Save and categorize content based on your preferences.

`Row(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


A single row in the confusion matrix.

## Attributes |
|
|---|---|
Name |
Description |
`actual_label` |
`str`
The original label of this row. |
`entries` |
`Sequence[`
Info describing predicted label distribution. |
