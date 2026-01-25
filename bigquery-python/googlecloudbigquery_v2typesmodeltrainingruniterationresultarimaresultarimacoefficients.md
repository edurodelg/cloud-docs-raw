---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaCoefficients
fetched_at: 2026-01-25T03:20:15.383780
---

# Class ArimaCoefficients (3.40.0)


      
      Save and categorize content based on your preferences.

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

## Attributes |
|
|---|---|
Name |
Description |
`auto_regressive_coefficients` |
`Sequence[float]`
Auto-regressive coefficients, an array of double. |
`moving_average_coefficients` |
`Sequence[float]`
Moving-average coefficients, an array of double. |
`intercept_coefficient` |
`float`
Intercept coefficient, just a double not an array. |