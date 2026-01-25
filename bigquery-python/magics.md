---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/magics
fetched_at: 2026-01-25T03:11:33.431586
---

# IPython Magics for BigQuery

To use these magics, you must first register them. Run the `%load_ext`

magic
in a Jupyter notebook cell.

```
%load_ext bigquery_magics
```


This makes the `%%bigquery`

magic available.

## Code Samples

Running a query:

```
%%bigquery
SELECT name, SUM(number) as count
FROM `bigquery-public-data.usa_names.usa_1910_current`
GROUP BY name
ORDER BY count DESC
LIMIT 3
```


Running a parameterized query:

```
%%bigquery --params {"corpus_name": "hamlet", "limit": 10}
SELECT word, SUM(word_count) as count
FROM `bigquery-public-data.samples.shakespeare`
WHERE corpus = @corpus_name
GROUP BY word
ORDER BY count DESC
LIMIT @limit
```