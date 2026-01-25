---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.TrainingRun.IterationResult.ArimaResult.ArimaModelInfo
fetched_at: 2026-01-25T02:13:59.507124
---

# Class ArimaModelInfo (3.40.0)


      
      Save and categorize content based on your preferences.

`ArimaModelInfo(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima model information.

## Attributes |
|
|---|---|
Name |
Description |
`non_seasonal_order` |
Non-seasonal order. |
`arima_coefficients` |
Arima coefficients. |
`arima_fitting_metrics` |
Arima fitting metrics. |
`has_drift` |
`bool`
Whether Arima model fitted with drift or not. It is always false when d is not 1. |
`time_series_id` |
`str`
The time_series_id value for this time series. It will be one of the unique values from the time_series_id_column specified during ARIMA model training. Only present when time_series_id_column training option was used. |
`time_series_ids` |
`Sequence[str]`
The tuple of time_series_ids identifying this time series. It will be one of the unique tuples of values present in the time_series_id_columns specified during ARIMA model training. Only present when time_series_id_columns training option was used and the order of values here are same as the order of time_series_id_columns. |
`seasonal_periods` |
`Sequence[`
Seasonal periods. Repeated because multiple periods are supported for one time series. |
`has_holiday_effect` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, holiday_effect is a part of time series decomposition result. |
`has_spikes_and_dips` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, spikes_and_dips is a part of time series decomposition result. |
`has_step_changes` |
`google.protobuf.wrappers_pb2.BoolValue`
If true, step_changes is a part of time series decomposition result. |