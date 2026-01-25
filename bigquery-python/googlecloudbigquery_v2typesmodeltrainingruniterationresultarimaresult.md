---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult
fetched_at: 2026-01-25T02:13:54.915119
---

# Class ArimaResult (3.40.0)


      
      Save and categorize content based on your preferences.

`ArimaResult(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


(Auto-)arima fitting result. Wrap everything in ArimaResult for easier refactoring if we want to use model-specific iteration results.

## Attributes |
|
|---|---|
Name |
Description |
`arima_model_info` |
`Sequence[`
This message is repeated because there are multiple arima models fitted in auto-arima. For non-auto-arima model, its size is one. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |

## Classes

### ArimaCoefficients

`ArimaCoefficients(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima coefficients.

### ArimaModelInfo

`ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima model information.