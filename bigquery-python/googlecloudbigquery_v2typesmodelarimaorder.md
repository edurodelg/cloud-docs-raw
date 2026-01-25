---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.ArimaOrder
fetched_at: 2026-01-25T02:12:36.478506
---

# Class ArimaOrder (3.40.0)


      
      Save and categorize content based on your preferences.

`ArimaOrder(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Arima order, can be used for both non-seasonal and seasonal parts.

## Attributes |
|
|---|---|
Name |
Description |
`p` |
`int`
Order of the autoregressive part. |
`d` |
`int`
Order of the differencing part. |
`q` |
`int`
Order of the moving-average part. |