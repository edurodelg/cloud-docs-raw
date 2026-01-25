---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.enums.RoundingMode
fetched_at: 2026-01-25T03:13:27.899999
---

# Class RoundingMode (3.40.0)


      
      Save and categorize content based on your preferences.

`RoundingMode(value)`


Rounding mode options that can be used when storing NUMERIC or BIGNUMERIC values.

ROUNDING_MODE_UNSPECIFIED: will default to using ROUND_HALF_AWAY_FROM_ZERO.

ROUND_HALF_AWAY_FROM_ZERO: rounds half values away from zero when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5, 1.6, 1.7, 1.8, 1.9 => 2

ROUND_HALF_EVEN: rounds half values to the nearest even value when applying precision and scale upon writing of NUMERIC and BIGNUMERIC values. For Scale: 0

- 1.1, 1.2, 1.3, 1.4 => 1
- 1.5 => 2
- 1.6, 1.7, 1.8, 1.9 => 2
- 2.5 => 2