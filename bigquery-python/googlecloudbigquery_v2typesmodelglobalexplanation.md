---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery_v2.types.Model.GlobalExplanation
fetched_at: 2026-01-25T02:13:08.988148
---

# Class GlobalExplanation (3.40.0)


      
      Save and categorize content based on your preferences.

`GlobalExplanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Global explanations containing the top most important features after training.

## Attributes |
|
|---|---|
Name |
Description |
`explanations` |
`Sequence[`
A list of the top global explanations. Sorted by absolute value of attribution in descending order. |
`class_label` |
`str`
Class label for this set of global explanations. Will be empty/null for binary logistic and linear regression models. Sorted alphabetically in descending order. |

## Classes

### Explanation

`Explanation(mapping=None, *, ignore_unknown_fields=False, **kwargs)`


Explanation for a single feature.