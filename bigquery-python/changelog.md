---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/changelog
fetched_at: 2026-01-25T02:04:53.361792
---

# Changelog

[3.40.0](https://github.com/googleapis/google-cloud-python/compare/google-cloud-bigquery-v3.39.0...google-cloud-bigquery-v3.40.0) (2026-01-08)

### Features

support load_table and list_rows with picosecond timestamp (#2351) (

[46764a59ca7a21ed14ad2c91eb7f98c302736c22](https://github.com/googleapis/google-cloud-python/commit/46764a59ca7a21ed14ad2c91eb7f98c302736c22))support timestamp_precision in table schema (#2333) (

[8d5785aea50b9f9e5b13bd4c91e8a08d6dac7778](https://github.com/googleapis/google-cloud-python/commit/8d5785aea50b9f9e5b13bd4c91e8a08d6dac7778))

[3.39.0](https://github.com/googleapis/google-cloud-python/compare/google-cloud-bigquery-v3.38.0...google-cloud-bigquery-v3.39.0) (2025-12-12)

### Documentation

- remove experimental annotations from GA features (#2303) (
[1f1f9d41e8a2c9016198d848ad3f1cbb88cf77b0](https://github.com/googleapis/google-cloud-python/commit/1f1f9d41e8a2c9016198d848ad3f1cbb88cf77b0))

### Features

adds support for Python runtime 3.14 (#2322) (

[6065e14c448cb430189982dd70025fa0575777ca](https://github.com/googleapis/google-cloud-python/commit/6065e14c448cb430189982dd70025fa0575777ca))Add ExternalRuntimeOptions to BigQuery routine (#2311) (

[fa76e310a16ea6cba0071ff1d767ca1c71514da7](https://github.com/googleapis/google-cloud-python/commit/fa76e310a16ea6cba0071ff1d767ca1c71514da7))

### Bug Fixes

include

`io.Base`

in the`PathType`

(#2323) ([b11e09cb6ee32e451b37eda66bece2220b9ceaba](https://github.com/googleapis/google-cloud-python/commit/b11e09cb6ee32e451b37eda66bece2220b9ceaba))honor custom

`retry`

in`job.result()`

(#2302) ([e118b029bbc89a5adbab83f39858c356c23665bf](https://github.com/googleapis/google-cloud-python/commit/e118b029bbc89a5adbab83f39858c356c23665bf))remove ambiguous error codes from query retries (#2308) (

[8bbd3d01026c493dfa5903b397d2b01c0e9bf43b](https://github.com/googleapis/google-cloud-python/commit/8bbd3d01026c493dfa5903b397d2b01c0e9bf43b))

[3.38.0](https://github.com/googleapis/python-bigquery/compare/v3.37.0...v3.38.0) (2025-09-15)

### Features

[3.37.0](https://github.com/googleapis/python-bigquery/compare/v3.36.0...v3.37.0) (2025-09-08)

### Features

### Bug Fixes

### Documentation

Clarify that the presence of

`XyzJob.errors`

doesn’t necessarily mean that the job has not completed or was unsuccessful ([#2278](https://github.com/googleapis/python-bigquery/issues/2278)) ([6e88d7d](https://github.com/googleapis/python-bigquery/commit/6e88d7dbe42ebfc35986da665d656b49ac481db4))Clarify the api_method arg for client.query() (

[#2277](https://github.com/googleapis/python-bigquery/issues/2277)) ([8a13c12](https://github.com/googleapis/python-bigquery/commit/8a13c12905ffcb3dbb6086a61df37556f0c2cd31))

[3.36.0](https://github.com/googleapis/python-bigquery/compare/v3.35.1...v3.36.0) (2025-08-20)

### Features

Add created/started/ended properties to RowIterator. (

[#2260](https://github.com/googleapis/python-bigquery/issues/2260)) ([0a95b24](https://github.com/googleapis/python-bigquery/commit/0a95b24192395cc3ccf801aa9bc318999873a2bf))Retry query jobs if

`jobBackendError`

or`jobInternalError`

are encountered ([#2256](https://github.com/googleapis/python-bigquery/issues/2256)) ([3deff1d](https://github.com/googleapis/python-bigquery/commit/3deff1d963980800e8b79fa3aaf5b712d4fd5062))

### Documentation

Add a TROUBLESHOOTING.md file with tips for logging (

[#2262](https://github.com/googleapis/python-bigquery/issues/2262)) ([b684832](https://github.com/googleapis/python-bigquery/commit/b68483227693ea68f6b12eacca2be1803cffb1d1))Update README to break infinite redirect loop (

[#2254](https://github.com/googleapis/python-bigquery/issues/2254)) ([8f03166](https://github.com/googleapis/python-bigquery/commit/8f031666114a826da2ad965f8ecd4727466cb480))

[3.35.1](https://github.com/googleapis/python-bigquery/compare/v3.35.0...v3.35.1) (2025-07-21)

### Documentation

[3.35.0](https://github.com/googleapis/python-bigquery/compare/v3.34.0...v3.35.0) (2025-07-15)

### Features

Add null_markers property to LoadJobConfig and CSVOptions (

[#2239](https://github.com/googleapis/python-bigquery/issues/2239)) ([289446d](https://github.com/googleapis/python-bigquery/commit/289446dd8c356d11a0b63b8e6275629b1ae5dc08))Adds dataset_view parameter to get_dataset method (

[#2198](https://github.com/googleapis/python-bigquery/issues/2198)) ([28a5750](https://github.com/googleapis/python-bigquery/commit/28a5750d455f0381548df6f9b1f7661823837d81))Adds date_format to load job and external config (

[#2231](https://github.com/googleapis/python-bigquery/issues/2231)) ([7d31828](https://github.com/googleapis/python-bigquery/commit/7d3182802deccfceb0646b87fc8d12275d0a569b))Adds source_column_match and associated tests (

[#2227](https://github.com/googleapis/python-bigquery/issues/2227)) ([6d5d236](https://github.com/googleapis/python-bigquery/commit/6d5d23685cd457d85955356705c1101e9ec3cdcd))Adds time_format and timestamp_format and associated tests (

[#2238](https://github.com/googleapis/python-bigquery/issues/2238)) ([371ad29](https://github.com/googleapis/python-bigquery/commit/371ad292df537278767dba71d81822ed57dd8e7d))Adds time_zone to external config and load job (

[#2229](https://github.com/googleapis/python-bigquery/issues/2229)) ([b2300d0](https://github.com/googleapis/python-bigquery/commit/b2300d032843512b7e4a5703377632fe60ef3f8d))

### Bug Fixes

Adds magics.context.project to eliminate issues with unit tests … (

[#2228](https://github.com/googleapis/python-bigquery/issues/2228)) ([27ff3a8](https://github.com/googleapis/python-bigquery/commit/27ff3a89a5f97305fa3ff673aa9183baa7df200f))Fix rows returned when both start_index and page_size are provided (

[#2181](https://github.com/googleapis/python-bigquery/issues/2181)) ([45643a2](https://github.com/googleapis/python-bigquery/commit/45643a2e20ce5d503118522dd195aeca00dec3bc))Make AccessEntry equality consistent with from_api_repr (

[#2218](https://github.com/googleapis/python-bigquery/issues/2218)) ([4941de4](https://github.com/googleapis/python-bigquery/commit/4941de441cb32cabeb55ec0320f305fb62551155))Update type hints for various BigQuery files (

[#2206](https://github.com/googleapis/python-bigquery/issues/2206)) ([b863291](https://github.com/googleapis/python-bigquery/commit/b86329188ba35e61871db82ae1d95d2a576eed1b))

### Documentation

[3.34.0](https://github.com/googleapis/python-bigquery/compare/v3.33.0...v3.34.0) (2025-05-27)

### Features

### Bug Fixes

### Documentation

[3.33.0](https://github.com/googleapis/python-bigquery/compare/v3.32.0...v3.33.0) (2025-05-19)

### Features

Add ability to set autodetect_schema query param in update_table (

[#2171](https://github.com/googleapis/python-bigquery/issues/2171)) ([57f940d](https://github.com/googleapis/python-bigquery/commit/57f940d957613b4d80fb81ea40a1177b73856189))Add dtype parameters to to_geodataframe functions (

[#2176](https://github.com/googleapis/python-bigquery/issues/2176)) ([ebfd0a8](https://github.com/googleapis/python-bigquery/commit/ebfd0a83d43bcb96f65f5669437220aa6138b766))

### Bug Fixes

Ensure AccessEntry equality and repr uses the correct

`entity_type`

([#2182](https://github.com/googleapis/python-bigquery/issues/2182)) ([0217637](https://github.com/googleapis/python-bigquery/commit/02176377d5e2fc25b5cd4f46aa6ebfb1b6a960a6))Ensure SchemaField.field_dtype returns a string (

[#2188](https://github.com/googleapis/python-bigquery/issues/2188)) ([7ec2848](https://github.com/googleapis/python-bigquery/commit/7ec2848379d5743bbcb36700a1153540c451e0e0))

[3.32.0](https://github.com/googleapis/python-bigquery/compare/v3.31.0...v3.32.0) (2025-05-12)

### Features

Add dataset access policy version attribute (

[#2169](https://github.com/googleapis/python-bigquery/issues/2169)) ([b7656b9](https://github.com/googleapis/python-bigquery/commit/b7656b97c1bd6c204d0508b1851d114719686655))Add preview support for incremental results (

[#2145](https://github.com/googleapis/python-bigquery/issues/2145)) ([22b80bb](https://github.com/googleapis/python-bigquery/commit/22b80bba9d0bed319fd3102e567906c9b458dd02))Adds condition class and assoc. unit tests (

[#2159](https://github.com/googleapis/python-bigquery/issues/2159)) ([a69d6b7](https://github.com/googleapis/python-bigquery/commit/a69d6b796d2edb6ba453980c9553bc9b206c5a6e))Support BigLakeConfiguration (managed Iceberg tables) (

[#2162](https://github.com/googleapis/python-bigquery/issues/2162)) ([a1c8e9a](https://github.com/googleapis/python-bigquery/commit/a1c8e9aaf60986924868d54a0ab0334e77002a39))Update the AccessEntry class with a new condition attribute and unit tests (

[#2163](https://github.com/googleapis/python-bigquery/issues/2163)) ([7301667](https://github.com/googleapis/python-bigquery/commit/7301667272dfbdd04b1a831418a9ad2d037171fb))

### Bug Fixes

`query()`

now warns when`job_id`

is set and the default`job_retry`

is ignored ([#2167](https://github.com/googleapis/python-bigquery/issues/2167)) ([ca1798a](https://github.com/googleapis/python-bigquery/commit/ca1798aaee2d5905fe688d3097f8ee5c989da333))Table iterator should not use bqstorage when page_size is not None (

[#2154](https://github.com/googleapis/python-bigquery/issues/2154)) ([e89a707](https://github.com/googleapis/python-bigquery/commit/e89a707b162182ededbf94cc9a0f7594bc2be475))

[3.31.0](https://github.com/googleapis/python-bigquery/compare/v3.30.0...v3.31.0) (2025-03-20)

### Features

Add query text and total bytes processed to RowIterator (

[#2140](https://github.com/googleapis/python-bigquery/issues/2140)) ([2d5f932](https://github.com/googleapis/python-bigquery/commit/2d5f9320d7103bc64c7ba496ba54bb0ef52b5605))Add support for Python 3.13 (

[0842aa1](https://github.com/googleapis/python-bigquery/commit/0842aa10967b1d8395cfb43e52c8ea091b381870))

### Bug Fixes

Adding property setter for table constraints,

[#1990](https://github.com/googleapis/python-bigquery/issues/1990)([#2092](https://github.com/googleapis/python-bigquery/issues/2092)) ([f8572dd](https://github.com/googleapis/python-bigquery/commit/f8572dd86595361bae82c3232b2c0d159690a7b7))Allow protobuf 6.x (

[0842aa1](https://github.com/googleapis/python-bigquery/commit/0842aa10967b1d8395cfb43e52c8ea091b381870))Avoid “Unable to determine type” warning with JSON columns in

`to_dataframe`

([#1876](https://github.com/googleapis/python-bigquery/issues/1876)) ([968020d](https://github.com/googleapis/python-bigquery/commit/968020d5be9d2a30b90d046eaf52f91bb2c70911))Remove setup.cfg configuration for creating universal wheels (

[#2146](https://github.com/googleapis/python-bigquery/issues/2146)) ([d7f7685](https://github.com/googleapis/python-bigquery/commit/d7f76853d598c354bfd2e65f5dde28dae97da0ec))

### Dependencies

[3.30.0](https://github.com/googleapis/python-bigquery/compare/v3.29.0...v3.30.0) (2025-02-26)

### Features

### Bug Fixes

### Dependencies

### Documentation

[3.29.0](https://github.com/googleapis/python-bigquery/compare/v3.28.0...v3.29.0) (2025-01-21)

### Features

### Bug Fixes

[3.28.0](https://github.com/googleapis/python-bigquery/compare/v3.27.0...v3.28.0) (2025-01-15)

### Features

Add property for

`allowNonIncrementalDefinition`

for materialized view ([#2084](https://github.com/googleapis/python-bigquery/issues/2084)) ([3359ef3](https://github.com/googleapis/python-bigquery/commit/3359ef37b90243bea2d9e68bb996fe5d736f304c))Add property for maxStaleness in table definitions (

[#2087](https://github.com/googleapis/python-bigquery/issues/2087)) ([729322c](https://github.com/googleapis/python-bigquery/commit/729322c2288a30464f2f135ba18b9c4aa7d2f0da))Adds ExternalCatalogDatasetOptions and tests (

[#2111](https://github.com/googleapis/python-bigquery/issues/2111)) ([b929a90](https://github.com/googleapis/python-bigquery/commit/b929a900d49e2c15897134209ed9de5fc7f238cd))Adds new input validation function similar to isinstance. (

[#2107](https://github.com/googleapis/python-bigquery/issues/2107)) ([a2bebb9](https://github.com/googleapis/python-bigquery/commit/a2bebb95c5ef32ac7c7cbe19c3e7a9412cbee60d))Preserve unknown fields from the REST API representation in

`SchemaField`

([#2097](https://github.com/googleapis/python-bigquery/issues/2097)) ([aaf1eb8](https://github.com/googleapis/python-bigquery/commit/aaf1eb85ada95ab866be0199812ea7f5c7f50766))Support setting max_stream_count when fetching query result (

[#2051](https://github.com/googleapis/python-bigquery/issues/2051)) ([d461297](https://github.com/googleapis/python-bigquery/commit/d4612979b812d2a835e47200f27a87a66bcb856a))

### Bug Fixes

### Documentation

[3.27.0](https://github.com/googleapis/python-bigquery/compare/v3.26.0...v3.27.0) (2024-11-01)

### Features

[3.26.0](https://github.com/googleapis/python-bigquery/compare/v3.25.0...v3.26.0) (2024-09-25)

### Features

### Bug Fixes

Add docfx to the presubmit configuration and delete docs-presubmit (

[#1995](https://github.com/googleapis/python-bigquery/issues/1995)) ([bd83cfd](https://github.com/googleapis/python-bigquery/commit/bd83cfd2eb25cec58d59af8048f5188d748b083d))Add warning when encountering unknown field types (

[#1989](https://github.com/googleapis/python-bigquery/issues/1989)) ([8f5a41d](https://github.com/googleapis/python-bigquery/commit/8f5a41d283a965ca161019588d3a3b2947b04b5b))Allow protobuf 5.x; require protobuf >=3.20.2; proto-plus >=1.22.3 (

[#1976](https://github.com/googleapis/python-bigquery/issues/1976)) ([57bf873](https://github.com/googleapis/python-bigquery/commit/57bf873474382cc2cb34243b704bc928fa1b64c6))Do not set job timeout extra property if None (

[#1987](https://github.com/googleapis/python-bigquery/issues/1987)) ([edcb79c](https://github.com/googleapis/python-bigquery/commit/edcb79ca69dba30d8102abebb9d53bc76e4882ee))Set pyarrow field nullable to False for a BigQuery field in REPEATED mode (

[#1999](https://github.com/googleapis/python-bigquery/issues/1999)) ([5352870](https://github.com/googleapis/python-bigquery/commit/5352870283ca7d4652aefc73f12645bcf6e1363c))

### Dependencies

### Documentation

[3.25.0](https://github.com/googleapis/python-bigquery/compare/v3.24.0...v3.25.0) (2024-06-17)

### Features

Add prefer_bqstorage_client option for Connection (

[#1945](https://github.com/googleapis/python-bigquery/issues/1945)) ([bfdeb3f](https://github.com/googleapis/python-bigquery/commit/bfdeb3fdbc1d5b26fcd3d1433abfb0be49d12018))Support load job option ColumnNameCharacterMap (

[#1952](https://github.com/googleapis/python-bigquery/issues/1952)) ([7e522ee](https://github.com/googleapis/python-bigquery/commit/7e522eea776cd9a74f8078c4236f63d5ff11f20e))

### Bug Fixes

[3.24.0](https://github.com/googleapis/python-bigquery/compare/v3.23.1...v3.24.0) (2024-06-04)

### Features

### Bug Fixes

### Performance Improvements

- If
`page_size`

or`max_results`

is set on`QueryJob.result()`

, use to download first page of results ([#1942](https://github.com/googleapis/python-bigquery/issues/1942)) ([3e7a48d](https://github.com/googleapis/python-bigquery/commit/3e7a48d36e3c7bf6abe1b5550097178f6ca6e174))

[3.23.1](https://github.com/googleapis/python-bigquery/compare/v3.23.0...v3.23.1) (2024-05-21)

### Performance Improvements

[3.23.0](https://github.com/googleapis/python-bigquery/compare/v3.22.0...v3.23.0) (2024-05-16)

### Features

### Bug Fixes

Add pyarrow version check for range support (

[#1914](https://github.com/googleapis/python-bigquery/issues/1914)) ([a86d7b9](https://github.com/googleapis/python-bigquery/commit/a86d7b96813f67fea28b46c5252416222edca9a6))Edit presubmit for to simplify configuration (

[#1915](https://github.com/googleapis/python-bigquery/issues/1915)) ([b739596](https://github.com/googleapis/python-bigquery/commit/b739596f37b8c00b375cc811c316b618097d761a))

[3.22.0](https://github.com/googleapis/python-bigquery/compare/v3.21.0...v3.22.0) (2024-04-19)

### Features

[3.21.0](https://github.com/googleapis/python-bigquery/compare/v3.20.1...v3.21.0) (2024-04-18)

### Features

### Bug Fixes

Remove duplicate key time_partitioning from Table._PROPERTY_TO_A… (

[#1898](https://github.com/googleapis/python-bigquery/issues/1898)) ([82ae908](https://github.com/googleapis/python-bigquery/commit/82ae908fbf3b2361343fff1859d3533383dc50ec))Retry query jobs that fail even with ambiguous

`jobs.getQueryResults`

REST errors ([#1903](https://github.com/googleapis/python-bigquery/issues/1903),[#1900](https://github.com/googleapis/python-bigquery/issues/1900)) ([1367b58](https://github.com/googleapis/python-bigquery/commit/1367b584b68d917ec325ce4383a0e9a36205b894))

### Performance Improvements

[3.20.1](https://github.com/googleapis/python-bigquery/compare/v3.20.0...v3.20.1) (2024-04-01)

### Bug Fixes

[3.20.0](https://github.com/googleapis/python-bigquery/compare/v3.19.0...v3.20.0) (2024-03-27)

### Features

### Bug Fixes

Update error logging when converting to pyarrow column fails (

[#1836](https://github.com/googleapis/python-bigquery/issues/1836)) ([0ac6e9b](https://github.com/googleapis/python-bigquery/commit/0ac6e9bf186945832f5dcdf5a4d95667b4da223e))Use an allowlist instead of denylist to determine when

`query_and_wait`

uses`jobs.query`

API ([#1869](https://github.com/googleapis/python-bigquery/issues/1869)) ([e265db6](https://github.com/googleapis/python-bigquery/commit/e265db6a6a37d13056dcaac240c2cf3975dfd644))

[3.19.0](https://github.com/googleapis/python-bigquery/compare/v3.18.0...v3.19.0) (2024-03-11)

### Features

### Bug Fixes

Add google-auth as a direct dependency (

[713ce2c](https://github.com/googleapis/python-bigquery/commit/713ce2c2f6ce9931f67cbbcd63ad436ad336ad26))**deps:**Require google-api-core>=1.34.1, >=2.11.0 ([713ce2c](https://github.com/googleapis/python-bigquery/commit/713ce2c2f6ce9931f67cbbcd63ad436ad336ad26))Supplementary fix to env-based universe resolution (

[#1844](https://github.com/googleapis/python-bigquery/issues/1844)) ([b818992](https://github.com/googleapis/python-bigquery/commit/b8189929b6008f7780214822062f8ed05d8d2a01))Supplementary fix to env-based universe resolution (

[#1847](https://github.com/googleapis/python-bigquery/issues/1847)) ([6dff50f](https://github.com/googleapis/python-bigquery/commit/6dff50f4fbc5aeb644383a4050dd5ffc05015ffe))

[3.18.0](https://github.com/googleapis/python-bigquery/compare/v3.17.2...v3.18.0) (2024-02-29)

### Features

### Bug Fixes

### Documentation

**samples:**Updates to urllib3 constraint for Python 3.7 ([#1834](https://github.com/googleapis/python-bigquery/issues/1834)) ([b099c32](https://github.com/googleapis/python-bigquery/commit/b099c32a83946a347560f6a71d08c3f263e56cb6))Update

`client_query_w_named_params.py`

to use`query_and_wait`

API ([#1782](https://github.com/googleapis/python-bigquery/issues/1782)) ([89dfcb6](https://github.com/googleapis/python-bigquery/commit/89dfcb6469d22e78003a70371a0938a6856e033c))

[3.17.2](https://github.com/googleapis/python-bigquery/compare/v3.17.1...v3.17.2) (2024-01-30)

### Bug Fixes

### Documentation

Update

`client_query_destination_table.py`

sample to use`query_and_wait`

([#1783](https://github.com/googleapis/python-bigquery/issues/1783)) ([68ebbe1](https://github.com/googleapis/python-bigquery/commit/68ebbe12d455ce8e9b1784fb11787c2fb842ef22))Update query_external_sheets_permanent_table.py to use query_and_wait API (

[#1778](https://github.com/googleapis/python-bigquery/issues/1778)) ([a7be88a](https://github.com/googleapis/python-bigquery/commit/a7be88adf8a480ee61aa79789cb53df1b79bb091))Update sample for query_to_arrow to use query_and_wait API (

[#1776](https://github.com/googleapis/python-bigquery/issues/1776)) ([dbf10de](https://github.com/googleapis/python-bigquery/commit/dbf10dee51a7635e9b98658f205ded2de087a06f))Update the query destination table legacy file to use query_and_wait API (

[#1775](https://github.com/googleapis/python-bigquery/issues/1775)) ([ef89f9e](https://github.com/googleapis/python-bigquery/commit/ef89f9e58c22b3af5a7757b69daa030116012350))Update to use

`query_and_wait`

in`client_query_w_positional_params.py`

([#1786](https://github.com/googleapis/python-bigquery/issues/1786)) ([410f71e](https://github.com/googleapis/python-bigquery/commit/410f71e6b6e755928e363ed89c1044e14b0db9cc))Update to use

`query_and_wait`

in`samples/client_query_w_timestamp_params.py`

([#1785](https://github.com/googleapis/python-bigquery/issues/1785)) ([ba36948](https://github.com/googleapis/python-bigquery/commit/ba3694852c13c8a29fe0f9d923353e82acfd4278))Update to_geodataframe to use query_and_wait functionality (

[#1800](https://github.com/googleapis/python-bigquery/issues/1800)) ([1298594](https://github.com/googleapis/python-bigquery/commit/12985942942b8f205ecd261fcdf620df9a640460))

[3.17.1](https://github.com/googleapis/python-bigquery/compare/v3.17.0...v3.17.1) (2024-01-24)

### Bug Fixes

Add pyarrow.large_strign to the _ARROW_SCALAR_IDS_TO_BQ map (

[#1796](https://github.com/googleapis/python-bigquery/issues/1796)) ([b402a6d](https://github.com/googleapis/python-bigquery/commit/b402a6df92e656aee10dd2c11c48f6ed93c74fd7))Retry ‘job exceeded rate limits’ for DDL queries (

[#1794](https://github.com/googleapis/python-bigquery/issues/1794)) ([39f33b2](https://github.com/googleapis/python-bigquery/commit/39f33b210ecbe9c2fd390825d29393c2d80257f5))

[3.17.0](https://github.com/googleapis/python-bigquery/compare/v3.16.0...v3.17.0) (2024-01-24)

### Features

### Bug Fixes

`query_and_wait`

now retains unknown query configuration`_properties`

([#1793](https://github.com/googleapis/python-bigquery/issues/1793)) ([4ba4342](https://github.com/googleapis/python-bigquery/commit/4ba434287a0a25f027e3b63a80f8881a9b16723e))Raise

`ValueError`

in`query_and_wait`

with wrong`job_config`

type ([4ba4342](https://github.com/googleapis/python-bigquery/commit/4ba434287a0a25f027e3b63a80f8881a9b16723e))

### Documentation

Update multiple samples to change query to query_and_wait (

[#1784](https://github.com/googleapis/python-bigquery/issues/1784)) ([d1161dd](https://github.com/googleapis/python-bigquery/commit/d1161dddde41a7d35b30033ccbf6984a5de640bd))Update the query with no cache sample to use query_and_wait API (

[#1770](https://github.com/googleapis/python-bigquery/issues/1770)) ([955a4cd](https://github.com/googleapis/python-bigquery/commit/955a4cd99e21cbca1b2f9c1dc6aa3fd8070cd61f))Updates

`query`

to`query and wait`

in samples/desktopapp/user_credentials.py ([#1787](https://github.com/googleapis/python-bigquery/issues/1787)) ([89f1299](https://github.com/googleapis/python-bigquery/commit/89f1299b3164b51fb0f29bc600a34ded59c10682))

[3.16.0](https://github.com/googleapis/python-bigquery/compare/v3.15.0...v3.16.0) (2024-01-12)

### Features

### Bug Fixes

[3.15.0](https://github.com/googleapis/python-bigquery/compare/v3.14.1...v3.15.0) (2024-01-09)

### Features

### Bug Fixes

Deserializing JSON subfields within structs fails (

[#1742](https://github.com/googleapis/python-bigquery/issues/1742)) ([0d93073](https://github.com/googleapis/python-bigquery/commit/0d930739c78b557db6cd48b38fe16eba93719c40))Due to upstream change in dataset, updates expected results (

[#1761](https://github.com/googleapis/python-bigquery/issues/1761)) ([132c14b](https://github.com/googleapis/python-bigquery/commit/132c14bbddfb61ea8bc408bef5e958e21b5b819c))Load_table_from_dataframe for higher scale decimal (

[#1703](https://github.com/googleapis/python-bigquery/issues/1703)) ([b9c8be0](https://github.com/googleapis/python-bigquery/commit/b9c8be0982c76187444300c414e0dda8b0ad105b))Updates types-protobuf version for mypy-samples nox session (

[#1764](https://github.com/googleapis/python-bigquery/issues/1764)) ([c0de695](https://github.com/googleapis/python-bigquery/commit/c0de6958e5761ad6ff532dd933b0f4387e18f1b9))

### Performance Improvements

[3.14.1](https://github.com/googleapis/python-bigquery/compare/v3.14.0...v3.14.1) (2023-12-13)

### Bug Fixes

[3.14.0](https://github.com/googleapis/python-bigquery/compare/v3.13.0...v3.14.0) (2023-12-08)

### Features

Add

`Client.query_and_wait`

which directly returns a`RowIterator`

of results ([#1722](https://github.com/googleapis/python-bigquery/issues/1722)) ([89a647e](https://github.com/googleapis/python-bigquery/commit/89a647e19fe5d7302c0a39bba77a155635c5c29d))Add

`job_id`

,`location`

,`project`

, and`query_id`

properties on`RowIterator`

([#1733](https://github.com/googleapis/python-bigquery/issues/1733)) ([494f275](https://github.com/googleapis/python-bigquery/commit/494f275ab2493dc7904f685c4d12e60bef51ab21))Add

`job_timeout_ms`

to job configuration classes ([#1675](https://github.com/googleapis/python-bigquery/issues/1675)) ([84d64cd](https://github.com/googleapis/python-bigquery/commit/84d64cdd157afef4a7bf7807e557d59452133434))Removed pkg_resources from all test files and moved importlib into pandas extra (

[#1726](https://github.com/googleapis/python-bigquery/issues/1726)) ([1f4ebb1](https://github.com/googleapis/python-bigquery/commit/1f4ebb1eca4f9380a31172fc8cb2fae125f8c5a2))

### Bug Fixes

`load_table_from_dataframe`

now assumes there may be local null values ([#1735](https://github.com/googleapis/python-bigquery/issues/1735)) ([f05dc69](https://github.com/googleapis/python-bigquery/commit/f05dc69a1f8c65ac32085bfcc6950c2c83f8a843))Ensure query job retry has longer deadline than API request deadline (

[#1734](https://github.com/googleapis/python-bigquery/issues/1734)) ([5573579](https://github.com/googleapis/python-bigquery/commit/55735791122f97b7f67cb962b489fd1f12210af5))Keep

`RowIterator.total_rows`

populated after iteration ([#1748](https://github.com/googleapis/python-bigquery/issues/1748)) ([8482f47](https://github.com/googleapis/python-bigquery/commit/8482f4759ce3c4b00fa06a7f306a2ac4d4ee8eb7))Move grpc, proto-plus and protobuf packages to extras (

[#1721](https://github.com/googleapis/python-bigquery/issues/1721)) ([5ce4d13](https://github.com/googleapis/python-bigquery/commit/5ce4d136af97b91fbe1cc56bba1021e50a9c8476))

### Performance Improvements

[3.13.0](https://github.com/googleapis/python-bigquery/compare/v3.12.0...v3.13.0) (2023-10-30)

### Features

### Bug Fixes

### Documentation

[3.12.0](https://github.com/googleapis/python-bigquery/compare/v3.11.4...v3.12.0) (2023-10-02)

### Features

Add

`Dataset.storage_billing_model`

setter, use`client.update_dataset(ds, fields=["storage_billing_model"])`

to update ([#1643](https://github.com/googleapis/python-bigquery/issues/1643)) ([5deba50](https://github.com/googleapis/python-bigquery/commit/5deba50b8c2d91d08bd5f5fb68742268c494b4a9))Widen retry predicate to include ServiceUnavailable (

[#1641](https://github.com/googleapis/python-bigquery/issues/1641)) ([3e021a4](https://github.com/googleapis/python-bigquery/commit/3e021a46d387a0e3cb69913a281062fc221bb926))

### Bug Fixes

Allow

`storage_billing_model`

to be explicitly set to`None`

to use project default value ([#1665](https://github.com/googleapis/python-bigquery/issues/1665)) ([514d3e1](https://github.com/googleapis/python-bigquery/commit/514d3e12e5131bd589dff08893fd89bf40338ba3))

### Documentation

[3.11.4](https://github.com/googleapis/python-bigquery/compare/v3.11.3...v3.11.4) (2023-07-19)

### Bug Fixes

[3.11.3](https://github.com/googleapis/python-bigquery/compare/v3.11.2...v3.11.3) (2023-06-27)

### Bug Fixes

[3.11.2](https://github.com/googleapis/python-bigquery/compare/v3.11.1...v3.11.2) (2023-06-21)

### Bug Fixes

[3.11.1](https://github.com/googleapis/python-bigquery/compare/v3.11.0...v3.11.1) (2023-06-09)

### Documentation

[3.11.0](https://github.com/googleapis/python-bigquery/compare/v3.10.0...v3.11.0) (2023-06-01)

### Features

### Bug Fixes

Filter None values from OpenTelemetry attributes (

[#1567](https://github.com/googleapis/python-bigquery/issues/1567)) ([9ea2e21](https://github.com/googleapis/python-bigquery/commit/9ea2e21c35783782993d1ad2d3b910bbe9981ce2))Raise most recent exception when not able to fetch query job after starting the job (

[#1362](https://github.com/googleapis/python-bigquery/issues/1362)) ([09cc1df](https://github.com/googleapis/python-bigquery/commit/09cc1df6babaf90ea0b0a6fd926f8013822a31ed))

[3.10.0](https://github.com/googleapis/python-bigquery/compare/v3.9.0...v3.10.0) (2023-04-18)

### Features

[3.9.0](https://github.com/googleapis/python-bigquery/compare/v3.8.0...v3.9.0) (2023-03-28)

### Features

### Bug Fixes

- Keyerror when the load_table_from_dataframe accesses a unmapped dtype dataframe index (
[#1535](https://github.com/googleapis/python-bigquery/issues/1535)) ([a69348a](https://github.com/googleapis/python-bigquery/commit/a69348a558f48cfc61d03d3e8bb7f9aee48bea86))

[3.8.0](https://github.com/googleapis/python-bigquery/compare/v3.7.0...v3.8.0) (2023-03-24)

### Features

Add bool, int, float, string dtype to to_dataframe (

[#1529](https://github.com/googleapis/python-bigquery/issues/1529)) ([5e4465d](https://github.com/googleapis/python-bigquery/commit/5e4465d0975f54e8da885006686d9431ff9c5653))Expose configuration property on CopyJob, ExtractJob, LoadJob, QueryJob (

[#1521](https://github.com/googleapis/python-bigquery/issues/1521)) ([8270a10](https://github.com/googleapis/python-bigquery/commit/8270a10df8f40750a7ac541a1781a71d7e79ce67))

### Bug Fixes

[3.7.0](https://github.com/googleapis/python-bigquery/compare/v3.6.0...v3.7.0) (2023-03-06)

### Features

Add

`connection_properties`

and`create_session`

to`LoadJobConfig`

([#1509](https://github.com/googleapis/python-bigquery/issues/1509)) ([cd0aaa1](https://github.com/googleapis/python-bigquery/commit/cd0aaa15960e9ca7a0aaf411c8e4990f95421816))Add default_query_job_config property and property setter to BQ client (

[#1511](https://github.com/googleapis/python-bigquery/issues/1511)) ([a23092c](https://github.com/googleapis/python-bigquery/commit/a23092cad834c6a016f455d46fefa13bb6cdbf0f))

### Documentation

[3.6.0](https://github.com/googleapis/python-bigquery/compare/v3.5.0...v3.6.0) (2023-02-22)

### Features

### Bug Fixes

Annotate optional integer parameters with optional type (

[#1487](https://github.com/googleapis/python-bigquery/issues/1487)) ([a190aaa](https://github.com/googleapis/python-bigquery/commit/a190aaa09ae73e8b6a83b7b213247f95fde57615))Removes scope to avoid unnecessary duplication (

[#1503](https://github.com/googleapis/python-bigquery/issues/1503)) ([665d7ba](https://github.com/googleapis/python-bigquery/commit/665d7ba74a1b45de1ef51cc75b6860125afc5fe6))

### Dependencies

- Update minimum google-cloud-core to 1.6.0 (
[a190aaa](https://github.com/googleapis/python-bigquery/commit/a190aaa09ae73e8b6a83b7b213247f95fde57615))

[3.5.0](https://github.com/googleapis/python-bigquery/compare/v3.4.2...v3.5.0) (2023-01-31)

### Features

### Documentation

Adds snippet for creating table with external data config (

[#1420](https://github.com/googleapis/python-bigquery/issues/1420)) ([f0ace2a](https://github.com/googleapis/python-bigquery/commit/f0ace2ac2307ef359511a235f80f5ce9e46264c1))Revise delete label table code sample, add TODO to clean up sni… (

[#1466](https://github.com/googleapis/python-bigquery/issues/1466)) ([0dab7d2](https://github.com/googleapis/python-bigquery/commit/0dab7d25ace4b63d2984485e7b0c5bb38f20476f))

[3.4.2](https://github.com/googleapis/python-bigquery/compare/v3.4.1...v3.4.2) (2023-01-13)

### Bug Fixes

### Dependencies

### Documentation

Create sample to write schema file from table (

[#1439](https://github.com/googleapis/python-bigquery/issues/1439)) ([093cc68](https://github.com/googleapis/python-bigquery/commit/093cc6852ada29898c4a4d047fd216544ef15bba))Created samples for load table and create table from schema file (

[#1436](https://github.com/googleapis/python-bigquery/issues/1436)) ([8ad2e5b](https://github.com/googleapis/python-bigquery/commit/8ad2e5bc1c04bf16fffe4c8773e722b68117c916))Revise get table labels code sample, add TODO to clean up snipp… (

[#1464](https://github.com/googleapis/python-bigquery/issues/1464)) ([b5ccbfe](https://github.com/googleapis/python-bigquery/commit/b5ccbfe4eee91d7f481d9708084cd29d0c85e666))

[3.4.1](https://github.com/googleapis/python-bigquery/compare/v3.4.0...v3.4.1) (2022-12-09)

### Documentation

### Dependencies

- make pyarrow and BQ Storage optional dependencies (
[e1aa921](https://github.com/googleapis/python-bigquery/commit/e1aa9218ad22f85c9a6cab8b61d013779376a582))

[3.4.0](https://github.com/googleapis/python-bigquery/compare/v3.3.6...v3.4.0) (2022-11-17)

### Features

Add

`reference_file_schema_uri`

to LoadJobConfig, ExternalConfig ([#1399](https://github.com/googleapis/python-bigquery/issues/1399)) ([931285f](https://github.com/googleapis/python-bigquery/commit/931285ff85842ab07a0ef2ff9db808181ea3c5e4))Add More Specific Type Annotations for Row Dictionaries (

[#1295](https://github.com/googleapis/python-bigquery/issues/1295)) ([eb49873](https://github.com/googleapis/python-bigquery/commit/eb49873176dee478617eb50472d44703abca53b5))

[3.3.6](https://github.com/googleapis/python-bigquery/compare/v3.3.4...v3.3.6) (2022-11-02)

### Features

### Bug Fixes

### Documentation

### Miscellaneous Chores

- release 3.3.6 (
[4fce1d9](https://github.com/googleapis/python-bigquery/commit/4fce1d93b1763703b115a0480a2b97021786aff7))

[3.3.4](https://github.com/googleapis/python-bigquery/compare/v3.3.3...v3.3.4) (2022-09-29)

### Bug Fixes

[3.3.3](https://github.com/googleapis/python-bigquery/compare/v3.3.2...v3.3.3) (2022-09-28)

### Bug Fixes

Refactors code to account for a tdqm code deprecation (

[#1357](https://github.com/googleapis/python-bigquery/issues/1357)) ([1369a9d](https://github.com/googleapis/python-bigquery/commit/1369a9d937b85d6a2a6bf9a672c71620648b1e3e))Validate opentelemetry span job attributes have values (

[#1327](https://github.com/googleapis/python-bigquery/issues/1327)) ([8287af1](https://github.com/googleapis/python-bigquery/commit/8287af1299169546f847126f03ae04e48890139e))

### Documentation

**samples:**uses function (create_job) more appropriate to the described sample intent ([5aeedaa](https://github.com/googleapis/python-bigquery/commit/5aeedaa2f4e6a0200d50521dfd90f39f9a24d0cc))

[3.3.2](https://github.com/googleapis/python-bigquery/compare/v3.3.1...v3.3.2) (2022-08-16)

### Bug Fixes

**deps:**require proto-plus >= 1.22.0 ([1de7a52](https://github.com/googleapis/python-bigquery/commit/1de7a52cb85d4876e4aa87346aff5725c8294c4e))

[3.3.1](https://github.com/googleapis/python-bigquery/compare/v3.3.0...v3.3.1) (2022-08-09)

### Bug Fixes

[3.3.0](https://github.com/googleapis/python-bigquery/compare/v3.2.0...v3.3.0) (2022-07-25)

### Features

### Bug Fixes

### Documentation

[3.2.0](https://github.com/googleapis/python-bigquery/compare/v3.1.0...v3.2.0) (2022-06-06)

### Features

### Bug Fixes

**deps:**proto-plus >= 1.15.0, <2.0.0dev ([ba58d3a](https://github.com/googleapis/python-bigquery/commit/ba58d3af80ca796be09c813529d3aadb79e0413c))**deps:**require packaging >= 14.3, <22.0.0dev ([ba58d3a](https://github.com/googleapis/python-bigquery/commit/ba58d3af80ca796be09c813529d3aadb79e0413c))**deps:**require protobuf>= 3.12.0, <4.0.0dev ([#1263](https://github.com/googleapis/python-bigquery/issues/1263)) ([ba58d3a](https://github.com/googleapis/python-bigquery/commit/ba58d3af80ca796be09c813529d3aadb79e0413c))

### Documentation

[3.1.0](https://github.com/googleapis/python-bigquery/compare/v3.0.1...v3.1.0) (2022-05-09)

### Features

refactor AccessEntry to use _properties pattern (

[#1125](https://github.com/googleapis/python-bigquery/issues/1125)) ([acd5612](https://github.com/googleapis/python-bigquery/commit/acd5612d2fc469633936dbc463ce4d70951e7fdd))support using BIGQUERY_EMULATOR_HOST environment variable (

[#1222](https://github.com/googleapis/python-bigquery/issues/1222)) ([39294b4](https://github.com/googleapis/python-bigquery/commit/39294b4950896b084573bedb4c5adc2b8d371eac))

### Bug Fixes

### Documentation

[3.0.1](https://github.com/googleapis/python-bigquery/compare/v3.0.0...v3.0.1) (2022-03-30)

### Bug Fixes

**deps:**raise exception when pandas is installed but db-dtypes is not ([#1191](https://github.com/googleapis/python-bigquery/issues/1191)) ([4333910](https://github.com/googleapis/python-bigquery/commit/433391097bae57dd12a93db18fc2bab573d8f128))**deps:**restore dependency on python-dateutil ([#1187](https://github.com/googleapis/python-bigquery/issues/1187)) ([212d7ec](https://github.com/googleapis/python-bigquery/commit/212d7ec1f0740d04c26fb3ceffc9a4dd9eed6756))

[3.0.0](https://github.com/googleapis/python-bigquery/compare/v2.34.3...v3.0.0) (2022-03-29)

### ⚠ BREAKING CHANGES

BigQuery Storage and pyarrow are required dependencies (#776)

use nullable

`Int64`

and`boolean`

dtypes in`to_dataframe`

(#786)destination tables are no-longer removed by

`create_job`

(#891)In

`to_dataframe`

, use`dbdate`

and`dbtime`

dtypes from db-dtypes package for BigQuery DATE and TIME columns (#972)automatically convert out-of-bounds dates in

`to_dataframe`

, remove`date_as_object`

argument (#972)mark the package as type-checked (#1058)

default to DATETIME type when loading timezone-naive datetimes from Pandas (#1061)

remove out-of-date BigQuery ML protocol buffers (#1178)


### Features

add

`api_method`

parameter to`Client.query`

to select`INSERT`

or`QUERY`

API ([#967](https://github.com/googleapis/python-bigquery/issues/967)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))default to DATETIME type when loading timezone-naive datetimes from Pandas (

[#1061](https://github.com/googleapis/python-bigquery/issues/1061)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))destination tables are no-longer removed by

`create_job`

([#891](https://github.com/googleapis/python-bigquery/issues/891)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))In

`to_dataframe`

, use`dbdate`

and`dbtime`

dtypes from db-dtypes package for BigQuery DATE and TIME columns ([#972](https://github.com/googleapis/python-bigquery/issues/972)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))use

`StandardSqlField`

class for`Model.feature_columns`

and`Model.label_columns`

([#1117](https://github.com/googleapis/python-bigquery/issues/1117)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))

### Bug Fixes

automatically convert out-of-bounds dates in

`to_dataframe`

, remove`date_as_object`

argument ([#972](https://github.com/googleapis/python-bigquery/issues/972)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))improve type annotations for mypy validation (

[#1081](https://github.com/googleapis/python-bigquery/issues/1081)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))remove out-of-date BigQuery ML protocol buffers (

[#1178](https://github.com/googleapis/python-bigquery/issues/1178)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))use nullable

`Int64`

and`boolean`

dtypes in`to_dataframe`

([#786](https://github.com/googleapis/python-bigquery/issues/786)) ([76d88fb](https://github.com/googleapis/python-bigquery/commit/76d88fbb1316317a61fa1a63c101bc6f42f23af8))

### Documentation

### Dependencies

[2.34.3](https://github.com/googleapis/python-bigquery/compare/v2.34.2...v2.34.3) (2022-03-29)

### Bug Fixes

[2.34.2](https://github.com/googleapis/python-bigquery/compare/v2.34.1...v2.34.2) (2022-03-05)

### Bug Fixes

**deps:**require google-api-core>=1.31.5, >=2.3.2 ([#1157](https://github.com/googleapis/python-bigquery/issues/1157)) ([0c15790](https://github.com/googleapis/python-bigquery/commit/0c15790720ff573a501cfe760dd74ee166e1a353))**deps:**require proto-plus>=1.15.0 ([0c15790](https://github.com/googleapis/python-bigquery/commit/0c15790720ff573a501cfe760dd74ee166e1a353))

[2.34.1](https://github.com/googleapis/python-bigquery/compare/v2.34.0...v2.34.1) (2022-03-02)

### Dependencies

[2.34.0](https://github.com/googleapis/python-bigquery/compare/v2.33.0...v2.34.0) (2022-02-18)

### Features

[2.33.0](https://github.com/googleapis/python-bigquery/compare/v2.32.0...v2.33.0) (2022-02-16)

### Features

### Bug Fixes

### Documentation

reference BigQuery REST API defaults in

`LoadJobConfig`

descrip… ([#1132](https://github.com/googleapis/python-bigquery/issues/1132)) ([18d9580](https://github.com/googleapis/python-bigquery/commit/18d958062721d6be81e7bd7a5bd66f277344a864))show common job properties in

`get_job`

and`cancel_job`

samples ([#1137](https://github.com/googleapis/python-bigquery/issues/1137)) ([8edc10d](https://github.com/googleapis/python-bigquery/commit/8edc10d019bd96defebc4f92a47774901e9b956f))

[2.32.0](https://github.com/googleapis/python-bigquery/compare/v2.31.0...v2.32.0) (2022-01-12)

### Features

### Bug Fixes

[2.31.0](https://www.github.com/googleapis/python-bigquery/compare/v2.30.1...v2.31.0) (2021-11-24)

### Features

### Bug Fixes

### Dependencies

[2.30.1](https://www.github.com/googleapis/python-bigquery/compare/v2.30.0...v2.30.1) (2021-11-04)

### Bug Fixes

### Documentation

show gcloud command to authorize against sheets (

[#1045](https://www.github.com/googleapis/python-bigquery/issues/1045)) ([20c9024](https://www.github.com/googleapis/python-bigquery/commit/20c9024b5760f7ae41301f4da54568496922cbe2))use stable URL for pandas intersphinx links (

[#1048](https://www.github.com/googleapis/python-bigquery/issues/1048)) ([73312f8](https://www.github.com/googleapis/python-bigquery/commit/73312f8f0f22ff9175a4f5f7db9bb438a496c164))

[2.30.0](https://www.github.com/googleapis/python-bigquery/compare/v2.29.0...v2.30.0) (2021-11-03)

### Features

### Documentation

add code samples for Jupyter/IPython magics (

[#1013](https://www.github.com/googleapis/python-bigquery/issues/1013)) ([61141ee](https://www.github.com/googleapis/python-bigquery/commit/61141ee0634024ad261d1595c95cd14a896fb87e))**samples:**add create external table with hive partitioning ([#1033](https://www.github.com/googleapis/python-bigquery/issues/1033)) ([d64f5b6](https://www.github.com/googleapis/python-bigquery/commit/d64f5b682854a2293244426316890df4ab1e079e))

[2.29.0](https://www.github.com/googleapis/python-bigquery/compare/v2.28.1...v2.29.0) (2021-10-27)

### Features

add

`QueryJob.schema`

property for dry run queries ([#1014](https://www.github.com/googleapis/python-bigquery/issues/1014)) ([2937fa1](https://www.github.com/googleapis/python-bigquery/commit/2937fa1386898766c561579fd39d42958182d260))add session and connection properties to QueryJobConfig (

[#1024](https://www.github.com/googleapis/python-bigquery/issues/1024)) ([e4c94f4](https://www.github.com/googleapis/python-bigquery/commit/e4c94f446c27eb474f30b033c1b62d11bd0acd98))add support for INTERVAL data type to

`list_rows`

([#840](https://www.github.com/googleapis/python-bigquery/issues/840)) ([e37380a](https://www.github.com/googleapis/python-bigquery/commit/e37380a959cbd5bb9cbbf6807f0a8ea147e0a713))allow queryJob.result() to be called on a dryRun (

[#1015](https://www.github.com/googleapis/python-bigquery/issues/1015)) ([685f06a](https://www.github.com/googleapis/python-bigquery/commit/685f06a5e7b5df17a53e9eb340ff04ecd1e51d1d))

### Documentation

document ScriptStatistics and other missing resource classes (

[#1023](https://www.github.com/googleapis/python-bigquery/issues/1023)) ([6679109](https://www.github.com/googleapis/python-bigquery/commit/66791093c61f262ea063d2a7950fc643915ee693))fix formatting of generated client docstrings (

[#1009](https://www.github.com/googleapis/python-bigquery/issues/1009)) ([f7b0ee4](https://www.github.com/googleapis/python-bigquery/commit/f7b0ee45a664295ccc9f209eeeac122af8de3c80))

### Dependencies

[2.28.1](https://www.github.com/googleapis/python-bigquery/compare/v2.28.0...v2.28.1) (2021-10-07)

### Bug Fixes

[2.28.0](https://www.github.com/googleapis/python-bigquery/compare/v2.27.1...v2.28.0) (2021-09-30)

### Features

### Documentation

[2.27.1](https://www.github.com/googleapis/python-bigquery/compare/v2.27.0...v2.27.1) (2021-09-27)

### Bug Fixes

[2.27.0](https://www.github.com/googleapis/python-bigquery/compare/v2.26.0...v2.27.0) (2021-09-24)

### Features

### Bug Fixes

Arrow extension-type metadata was not set when calling the REST API or when there are no rows (

[#946](https://www.github.com/googleapis/python-bigquery/issues/946)) ([864383b](https://www.github.com/googleapis/python-bigquery/commit/864383bc01636b3774f7da194587b8b7edd0383d))disambiguate missing policy tags from explicitly unset policy tags (

[#983](https://www.github.com/googleapis/python-bigquery/issues/983)) ([f83c00a](https://www.github.com/googleapis/python-bigquery/commit/f83c00acead70fc0ce9959eefb133a672d816277))

### Documentation

[2.26.0](https://www.github.com/googleapis/python-bigquery/compare/v2.25.2...v2.26.0) (2021-09-01)

### Features

### Bug Fixes

[2.25.2](https://www.github.com/googleapis/python-bigquery/compare/v2.25.1...v2.25.2) (2021-08-31)

### Bug Fixes

error inserting DataFrame with REPEATED field (

[#925](https://www.github.com/googleapis/python-bigquery/issues/925)) ([656d2fa](https://www.github.com/googleapis/python-bigquery/commit/656d2fa6f870573a21235c83463752a2d084caba))underscores weren’t allowed in struct field names when passing parameters to the DB API (

[#930](https://www.github.com/googleapis/python-bigquery/issues/930)) ([fcb0bc6](https://www.github.com/googleapis/python-bigquery/commit/fcb0bc68c972c2c98bb8542f54e9228308177ecb))

### Documentation

[2.25.1](https://www.github.com/googleapis/python-bigquery/compare/v2.25.0...v2.25.1) (2021-08-25)

### Bug Fixes

[2.25.0](https://www.github.com/googleapis/python-bigquery/compare/v2.24.1...v2.25.0) (2021-08-24)

### Features

[2.24.1](https://www.github.com/googleapis/python-bigquery/compare/v2.24.0...v2.24.1) (2021-08-13)

### Bug Fixes

[2.24.0](https://www.github.com/googleapis/python-bigquery/compare/v2.23.3...v2.24.0) (2021-08-11)

### Features

make the same

`Table\*`

instances equal to each other ([#867](https://www.github.com/googleapis/python-bigquery/issues/867)) ([c1a3d44](https://www.github.com/googleapis/python-bigquery/commit/c1a3d4435739a21d25aa154145e36d3a7c42eeb6))support

`ScalarQueryParameterType`

for`type_`

argument in`ScalarQueryParameter`

constructor ([#850](https://www.github.com/googleapis/python-bigquery/issues/850)) ([93d15e2](https://www.github.com/googleapis/python-bigquery/commit/93d15e2e5405c2cc6d158c4e5737361344193dbc))

### Bug Fixes

[2.23.3](https://www.github.com/googleapis/python-bigquery/compare/v2.23.2...v2.23.3) (2021-08-06)

### Bug Fixes

[2.23.2](https://www.github.com/googleapis/python-bigquery/compare/v2.23.1...v2.23.2) (2021-07-29)

### Dependencies

[2.23.1](https://www.github.com/googleapis/python-bigquery/compare/v2.23.0...v2.23.1) (2021-07-28)

### Bug Fixes

[2.23.0](https://www.github.com/googleapis/python-bigquery/compare/v2.22.1...v2.23.0) (2021-07-27)

### Features

### Bug Fixes

### Documentation

[2.22.1](https://www.github.com/googleapis/python-bigquery/compare/v2.22.0...v2.22.1) (2021-07-22)

### Bug Fixes

### Documentation

[2.22.0](https://www.github.com/googleapis/python-bigquery/compare/v2.21.0...v2.22.0) (2021-07-19)

### Features

add

`LoadJobConfig.projection_fields`

to select DATASTORE_BACKUP fields ([#736](https://www.github.com/googleapis/python-bigquery/issues/736)) ([c45a738](https://www.github.com/googleapis/python-bigquery/commit/c45a7380871af3dfbd3c45524cb606c60e1a01d1))add standard sql table type, update scalar type enums (

[#777](https://www.github.com/googleapis/python-bigquery/issues/777)) ([b8b5433](https://www.github.com/googleapis/python-bigquery/commit/b8b5433898ec881f8da1303614780a660d94733a))add support for user defined Table View Functions (

[#724](https://www.github.com/googleapis/python-bigquery/issues/724)) ([8c7b839](https://www.github.com/googleapis/python-bigquery/commit/8c7b839a6ac1491c1c3b6b0e8755f4b70ed72ee3))

### Bug Fixes

### Dependencies

### Documentation

[2.21.0](https://www.github.com/googleapis/python-bigquery/compare/v2.20.0...v2.21.0) (2021-07-12)

### Features

Add max_results parameter to some of the

`QueryJob`

methods. ([#698](https://www.github.com/googleapis/python-bigquery/issues/698)) ([2a9618f](https://www.github.com/googleapis/python-bigquery/commit/2a9618f4daaa4a014161e1a2f7376844eec9e8da))Enable unsetting policy tags on schema fields. (

[#703](https://www.github.com/googleapis/python-bigquery/issues/703)) ([18bb443](https://www.github.com/googleapis/python-bigquery/commit/18bb443c7acd0a75dcb57d9aebe38b2d734ff8c7))Make it easier to disable best-effort deduplication with streaming inserts. (

[#734](https://www.github.com/googleapis/python-bigquery/issues/734)) ([1246da8](https://www.github.com/googleapis/python-bigquery/commit/1246da86b78b03ca1aa2c45ec71649e294cfb2f1))

### Bug Fixes

### Documentation

[2.20.0](https://www.github.com/googleapis/python-bigquery/compare/v2.19.0...v2.20.0) (2021-06-07)

### Features

[2.19.0](https://www.github.com/googleapis/python-bigquery/compare/v2.18.0...v2.19.0) (2021-06-06)

### Features

- list_tables, list_projects, list_datasets, list_models, list_routines, and list_jobs now accept a page_size parameter to control page size (
[#686](https://www.github.com/googleapis/python-bigquery/issues/686)) ([1f1c4b7](https://www.github.com/googleapis/python-bigquery/commit/1f1c4b7ba4390fc4c5c8186bc22b83b45304ca06))

[2.18.0](https://www.github.com/googleapis/python-bigquery/compare/v2.17.0...v2.18.0) (2021-06-02)

### Features

[2.17.0](https://www.github.com/googleapis/python-bigquery/compare/v2.16.1...v2.17.0) (2021-05-21)

### Features

detect obsolete BQ Storage extra at runtime (

[#666](https://www.github.com/googleapis/python-bigquery/issues/666)) ([bd7dbda](https://www.github.com/googleapis/python-bigquery/commit/bd7dbdae5c972b16bafc53c67911eeaa3255a880))Support parameterized NUMERIC, BIGNUMERIC, STRING, and BYTES types (

[#673](https://www.github.com/googleapis/python-bigquery/issues/673)) ([45421e7](https://www.github.com/googleapis/python-bigquery/commit/45421e73bfcddb244822e6a5cd43be6bd1ca2256))

### Bug Fixes

[2.16.1](https://www.github.com/googleapis/python-bigquery/compare/v2.16.0...v2.16.1) (2021-05-12)

### Bug Fixes

[2.16.0](https://www.github.com/googleapis/python-bigquery/compare/v2.15.0...v2.16.0) (2021-05-05)

### Features

### Dependencies

[2.15.0](https://www.github.com/googleapis/python-bigquery/compare/v2.14.0...v2.15.0) (2021-04-29)

### Features

### Bug Fixes

add DECIMAL and BIGDECIMAL as aliases for NUMERIC and BIGNUMERIC (

[#638](https://www.github.com/googleapis/python-bigquery/issues/638)) ([aa59023](https://www.github.com/googleapis/python-bigquery/commit/aa59023317b1c63720fb717b3544f755652da58d))The DB API Binary function accepts bytes data (

[#630](https://www.github.com/googleapis/python-bigquery/issues/630)) ([4396e70](https://www.github.com/googleapis/python-bigquery/commit/4396e70771af6889d3242c37c5ff2e80241023a2))

[2.14.0](https://www.github.com/googleapis/python-bigquery/compare/v2.13.1...v2.14.0) (2021-04-26)

### Features

accept DatasetListItem where DatasetReference is accepted (

[#597](https://www.github.com/googleapis/python-bigquery/issues/597)) ([c8b5581](https://www.github.com/googleapis/python-bigquery/commit/c8b5581ea3c94005d69755c4a3b5a0d8900f3fe2))accept job object as argument to

`get_job`

and`cancel_job`

([#617](https://www.github.com/googleapis/python-bigquery/issues/617)) ([f75dcdf](https://www.github.com/googleapis/python-bigquery/commit/f75dcdf3943b87daba60011c9a3b42e34ff81910))add

`Client.delete_job_metadata`

method to remove job metadata ([#610](https://www.github.com/googleapis/python-bigquery/issues/610)) ([0abb566](https://www.github.com/googleapis/python-bigquery/commit/0abb56669c097c59fbffce007c702e7a55f2d9c1))add

`max_queue_size`

argument to`RowIterator.to_dataframe_iterable`

([#575](https://www.github.com/googleapis/python-bigquery/issues/575)) ([f95f415](https://www.github.com/googleapis/python-bigquery/commit/f95f415d3441b3928f6cc705cb8a75603d790fd6))retry google.auth TransportError by default (

[#624](https://www.github.com/googleapis/python-bigquery/issues/624)) ([34ecc3f](https://www.github.com/googleapis/python-bigquery/commit/34ecc3f1ca0ff073330c0c605673d89b43af7ed9))use pyarrow stream compression, if available (

[#593](https://www.github.com/googleapis/python-bigquery/issues/593)) ([dde9dc5](https://www.github.com/googleapis/python-bigquery/commit/dde9dc5114c2311fb76fafc5b222fff561e8abf1))

### Bug Fixes

consistent percents handling in DB API query (

[#619](https://www.github.com/googleapis/python-bigquery/issues/619)) ([6502a60](https://www.github.com/googleapis/python-bigquery/commit/6502a602337ae562652a20b20270949f2c9d5073))unsetting clustering fields on Table is now possible (

[#622](https://www.github.com/googleapis/python-bigquery/issues/622)) ([33a871f](https://www.github.com/googleapis/python-bigquery/commit/33a871f06329f9bf5a6a92fab9ead65bf2bee75d))

### Documentation

[2.13.1](https://www.github.com/googleapis/python-bigquery/compare/v2.13.0...v2.13.1) (2021-03-23)

### Bug Fixes

[2.13.0](https://www.github.com/googleapis/python-bigquery/compare/v2.12.0...v2.13.0) (2021-03-22)

### Features

### Bug Fixes

avoid overly strict dependency on pyarrow 3.x (

[#564](https://www.github.com/googleapis/python-bigquery/issues/564)) ([97ee6ec](https://www.github.com/googleapis/python-bigquery/commit/97ee6ec6cd4bc9f833cd506dc6d244d103654cfd))avoid policy tags 403 error in

`load_table_from_dataframe`

([#557](https://www.github.com/googleapis/python-bigquery/issues/557)) ([84e646e](https://www.github.com/googleapis/python-bigquery/commit/84e646e6b7087a1626e56ad51eeb130f4ddfa2fb))

[2.12.0](https://www.github.com/googleapis/python-bigquery/compare/v2.11.0...v2.12.0) (2021-03-16)

### Features

### Bug Fixes

[2.11.0](https://www.github.com/googleapis/python-bigquery/compare/v2.10.0...v2.11.0) (2021-03-09)

### Features

[2.10.0](https://www.github.com/googleapis/python-bigquery/compare/v2.9.0...v2.10.0) (2021-02-25)

### Features

### Bug Fixes

error using empty array of structs parameter (

[#474](https://www.github.com/googleapis/python-bigquery/issues/474)) ([c1d15f4](https://www.github.com/googleapis/python-bigquery/commit/c1d15f4e5da4b7e10c00afffd59a5c7f3ded027a))QueryJob.exception()

*returns*the errors, not raises them ([#467](https://www.github.com/googleapis/python-bigquery/issues/467)) ([d763279](https://www.github.com/googleapis/python-bigquery/commit/d7632799769248b09a8558ba18f5025ebdd9675a))

### Documentation

[2.9.0](https://www.github.com/googleapis/python-bigquery/compare/v2.8.0...v2.9.0) (2021-02-18)

### Features

### Documentation

[2.8.0](https://www.github.com/googleapis/python-bigquery/compare/v2.7.0...v2.8.0) (2021-02-08)

### Features

### Bug Fixes

[2.7.0](https://www.github.com/googleapis/python-bigquery/compare/v2.6.2...v2.7.0) (2021-01-27)

### Bug Fixes

invalid conversion of timezone-aware datetime values to JSON (

[#480](https://www.github.com/googleapis/python-bigquery/issues/480)) ([61b4385](https://www.github.com/googleapis/python-bigquery/commit/61b438523d305ce66a68fde7cb49e9abbf0a8d1d))reading the labels attribute on Job instances (

[#471](https://www.github.com/googleapis/python-bigquery/issues/471)) ([80944f0](https://www.github.com/googleapis/python-bigquery/commit/80944f080bcc4fda870a6daf1d884de616d39ae7))use explicitly given project over the client’s default project for load jobs (

[#482](https://www.github.com/googleapis/python-bigquery/issues/482)) ([530e1e8](https://www.github.com/googleapis/python-bigquery/commit/530e1e8d8fe8939e914a78ff1b220907c1b87af7))

### Dependencies

[2.6.2](https://www.github.com/googleapis/python-bigquery/compare/v2.6.1...v2.6.2) (2021-01-11)

### Bug Fixes

add minimum timeout to getQueryResults API requests (

[#444](https://www.github.com/googleapis/python-bigquery/issues/444)) ([015a73e](https://www.github.com/googleapis/python-bigquery/commit/015a73e1839e3427408ef6e0f879717d9ddbdb61))use debug logging level for OpenTelemetry message (

[#442](https://www.github.com/googleapis/python-bigquery/issues/442)) ([7ea6b7c](https://www.github.com/googleapis/python-bigquery/commit/7ea6b7c2469d2415192cfdacc379e38e49d24775))

### Documentation

[2.6.1](https://www.github.com/googleapis/python-bigquery/compare/v2.6.0...v2.6.1) (2020-12-09)

### Bug Fixes

### Documentation

[2.6.0](https://www.github.com/googleapis/python-bigquery/compare/v2.5.0...v2.6.0) (2020-12-07)

### Features

add support for materialized views (

[#408](https://www.github.com/googleapis/python-bigquery/issues/408)) ([57ffc66](https://www.github.com/googleapis/python-bigquery/commit/57ffc665319331e0a00583d5d652fd14a510cf2a)), closes[#407](https://www.github.com/googleapis/python-bigquery/issues/407)convert

`BIGNUMERIC`

values to decimal objects ([#414](https://www.github.com/googleapis/python-bigquery/issues/414)) ([d472d2d](https://www.github.com/googleapis/python-bigquery/commit/d472d2d2b33e40b954652d31476dea8c90e6a2dc)), closes[#367](https://www.github.com/googleapis/python-bigquery/issues/367)support CSV format in

`load_table_from_dataframe`

pandas connector ([#399](https://www.github.com/googleapis/python-bigquery/issues/399)) ([0046742](https://www.github.com/googleapis/python-bigquery/commit/0046742abdd2b5eab3c3e935316f91e7eef44d44))

### Bug Fixes

### Documentation

[2.5.0](https://www.github.com/googleapis/python-bigquery/compare/v2.4.0...v2.5.0) (2020-12-02)

### Features

### Bug Fixes

### Performance Improvements

### Documentation

### Dependencies

[2.4.0](https://www.github.com/googleapis/python-bigquery/compare/v2.3.1...v2.4.0) (2020-11-16)

### Features

### Bug Fixes

### Performance Improvements

avoid extra API calls from

`to_dataframe`

if all rows are cached ([#384](https://www.github.com/googleapis/python-bigquery/issues/384)) ([c52b317](https://www.github.com/googleapis/python-bigquery/commit/c52b31789998fc0dfde07c3296650c85104d719d))cache first page of

`jobs.getQueryResults`

rows ([#374](https://www.github.com/googleapis/python-bigquery/issues/374)) ([86f6a51](https://www.github.com/googleapis/python-bigquery/commit/86f6a516d1c7c5dc204ab085ea2578793e6561ff))

### Dependencies

## 2.3.1

11-05-2020 09:27 PST

### Internal / Testing Changes

- update
`google.cloud.bigquery.__version__`


[2.3.0](https://www.github.com/googleapis/python-bigquery/compare/v2.2.0...v2.3.0) (2020-11-04)

### Features

### Bug Fixes

add missing spaces in opentelemetry log message (

[#360](https://www.github.com/googleapis/python-bigquery/issues/360)) ([4f326b1](https://www.github.com/googleapis/python-bigquery/commit/4f326b1ca4411cfbf5ded86955a963d3e05a409f))**dbapi:**avoid running % format with no query parameters ([#348](https://www.github.com/googleapis/python-bigquery/issues/348)) ([5dd1a5e](https://www.github.com/googleapis/python-bigquery/commit/5dd1a5e77f13b8e576e917069e247c5390a81900))create_job method accepts dictionary arguments (

[#300](https://www.github.com/googleapis/python-bigquery/issues/300)) ([155bacc](https://www.github.com/googleapis/python-bigquery/commit/155bacc156f181384ca6dba699ab83d0398176d1))

### Performance Improvements

### Documentation

[2.2.0](https://www.github.com/googleapis/python-bigquery/compare/v2.1.0...v2.2.0) (2020-10-19)

### Features

add support for listing arima, automl, boosted tree, DNN, and matrix factorization models (

[#328](https://www.github.com/googleapis/python-bigquery/issues/328)) ([502a092](https://www.github.com/googleapis/python-bigquery/commit/502a0926018abf058cb84bd18043c25eba15a2cc))add timeout paramter to load_table_from_file and it dependent methods (

[#327](https://www.github.com/googleapis/python-bigquery/issues/327)) ([b0dd892](https://www.github.com/googleapis/python-bigquery/commit/b0dd892176e31ac25fddd15554b5bfa054299d4d))allow client options to be set in magics context (

[#322](https://www.github.com/googleapis/python-bigquery/issues/322)) ([5178b55](https://www.github.com/googleapis/python-bigquery/commit/5178b55682f5e264bfc082cde26acb1fdc953a18))

### Bug Fixes

make TimePartitioning repr evaluable (

[#110](https://www.github.com/googleapis/python-bigquery/issues/110)) ([20f473b](https://www.github.com/googleapis/python-bigquery/commit/20f473bfff5ae98377f5d9cdf18bfe5554d86ff4)), closes[#109](https://www.github.com/googleapis/python-bigquery/issues/109)use version.py instead of pkg_resources.get_distribution (

[#307](https://www.github.com/googleapis/python-bigquery/issues/307)) ([b8f502b](https://www.github.com/googleapis/python-bigquery/commit/b8f502b14f21d1815697e4d57cf1225dfb4a7c5e))

### Performance Improvements

### Documentation

update clustering field docstrings (

[#286](https://www.github.com/googleapis/python-bigquery/issues/286)) ([5ea1ece](https://www.github.com/googleapis/python-bigquery/commit/5ea1ece2d911cdd1f3d9549ee01559ce8ed8269a)), closes[#285](https://www.github.com/googleapis/python-bigquery/issues/285)update snippets samples to support version 2.0 (

[#309](https://www.github.com/googleapis/python-bigquery/issues/309)) ([61634be](https://www.github.com/googleapis/python-bigquery/commit/61634be9bf9e3df7589fc1bfdbda87288859bb13))

### Dependencies

[2.1.0](https://www.github.com/googleapis/python-bigquery/compare/v2.0.0...v2.1.0) (2020-10-08)

### Features

### Bug Fixes

### Performance Improvements

### Documentation

## 2.0.0

09-30-2020 14:51 PDT

### Implementation Changes

- Transition the library to microgenerator. (
[#278](https://github.com/googleapis/python-bigquery/pull/278)) This is a**breaking change**that**drops support for Python 2.7 and 3.5**and brings a few other changes. See[migration guide](https://googleapis.dev/python/bigquery/latest/UPGRADING.html)for more info.

### Internal / Testing Changes

[1.28.0](https://www.github.com/googleapis/python-bigquery/compare/v1.27.2...v1.28.0) (2020-09-22)

### Features

add custom cell magic parser to handle complex

`--params`

values ([#213](https://www.github.com/googleapis/python-bigquery/issues/213)) ([dcfbac2](https://www.github.com/googleapis/python-bigquery/commit/dcfbac267fbf66d189b0cc7e76f4712122a74b7b))expose require_partition_filter for hive_partition (

[#257](https://www.github.com/googleapis/python-bigquery/issues/257)) ([aa1613c](https://www.github.com/googleapis/python-bigquery/commit/aa1613c1bf48c7efb999cb8b8c422c80baf1950b))

### Bug Fixes

### Documentation

[1.27.2](https://www.github.com/googleapis/python-bigquery/compare/v1.27.1...v1.27.2) (2020-08-18)

### Bug Fixes

[1.27.1](https://www.github.com/googleapis/python-bigquery/compare/v1.27.0...v1.27.1) (2020-08-18)

### Bug Fixes

[1.27.0](https://www.github.com/googleapis/python-bigquery/compare/v1.26.1...v1.27.0) (2020-08-15)

### Features

### Bug Fixes

converting to dataframe with out of bounds timestamps (

[#209](https://www.github.com/googleapis/python-bigquery/issues/209)) ([8209203](https://www.github.com/googleapis/python-bigquery/commit/8209203e967f0624ad306166c0af6f6f1027c550)), closes[#168](https://www.github.com/googleapis/python-bigquery/issues/168)raise error if inserting rows with unknown fields (

[#163](https://www.github.com/googleapis/python-bigquery/issues/163)) ([8fe7254](https://www.github.com/googleapis/python-bigquery/commit/8fe725429541eed34ddc01cffc8b1ee846c14162))

[1.26.1](https://www.github.com/googleapis/python-bigquery/compare/v1.26.0...v1.26.1) (2020-07-25)

### Documentation

- Migrated code samples from
[https://github.com/GoogleCloudPlatform/python-docs-samples](https://github.com/GoogleCloudPlatform/python-docs-samples)

### Bug Fixes

### Dependencies

- Updated version constraints on grmp dependency in anticipation of 1.0.0 release
(
[#189](https://github.com/googleapis/python-bigquery/pull/189))

[1.26.0](https://www.github.com/googleapis/python-bigquery/compare/v1.25.0...v1.26.0) (2020-07-20)

### Features

use BigQuery Storage client by default (if dependencies available) (

[#55](https://www.github.com/googleapis/python-bigquery/issues/55)) ([e75ff82](https://www.github.com/googleapis/python-bigquery/commit/e75ff8297c65981545b097f75a17cf9e78ac6772)), closes[#91](https://www.github.com/googleapis/python-bigquery/issues/91)**bigquery:**add**eq**method for class PartitionRange and RangePartitioning ([#162](https://www.github.com/googleapis/python-bigquery/issues/162)) ([0d2a88d](https://www.github.com/googleapis/python-bigquery/commit/0d2a88d8072154cfc9152afd6d26a60ddcdfbc73))**bigquery:**expose date_as_object parameter to users ([#150](https://www.github.com/googleapis/python-bigquery/issues/150)) ([a2d5ce9](https://www.github.com/googleapis/python-bigquery/commit/a2d5ce9e97992318d7dc85c51c053cab74e25a11))**bigquery:**expose date_as_object parameter to users ([#150](https://www.github.com/googleapis/python-bigquery/issues/150)) ([cbd831e](https://www.github.com/googleapis/python-bigquery/commit/cbd831e08024a67148723afd49e1db085e0a862c))

### Bug Fixes

### Documentation

**bigquery:**add client thread-safety documentation ([#132](https://www.github.com/googleapis/python-bigquery/issues/132)) ([fce76b3](https://www.github.com/googleapis/python-bigquery/commit/fce76b3776472b1da798df862a3405e659e35bab))**bigquery:**add docstring for conflict exception ([#171](https://www.github.com/googleapis/python-bigquery/issues/171)) ([9c3409b](https://www.github.com/googleapis/python-bigquery/commit/9c3409bb06218bf499620544f8e92802df0cce47))**bigquery:**consistent use of optional keyword ([#153](https://www.github.com/googleapis/python-bigquery/issues/153)) ([79d8c61](https://www.github.com/googleapis/python-bigquery/commit/79d8c61064cca18b596a24b6f738c7611721dd5c))

[1.25.0](https://www.github.com/googleapis/python-bigquery/compare/v1.24.0...v1.25.0) (2020-06-06)

### Features

add BigQuery storage client support to DB API (

[#36](https://www.github.com/googleapis/python-bigquery/issues/36)) ([ba9b2f8](https://www.github.com/googleapis/python-bigquery/commit/ba9b2f87e36320d80f6f6460b77e6daddb0fa214))**bigquery:**add support of model for extract job ([#71](https://www.github.com/googleapis/python-bigquery/issues/71)) ([4a7a514](https://www.github.com/googleapis/python-bigquery/commit/4a7a514659a9f6f9bbd8af46bab3f8782d6b4b98))add HOUR support for time partitioning interval (

[#91](https://www.github.com/googleapis/python-bigquery/issues/91)) ([0dd90b9](https://www.github.com/googleapis/python-bigquery/commit/0dd90b90e3714c1d18f8a404917a9454870e338a))**bigquery:**expose start index parameter for query result ([#121](https://www.github.com/googleapis/python-bigquery/issues/121)) ([be86de3](https://www.github.com/googleapis/python-bigquery/commit/be86de330a3c3801653a0ccef90e3d9bdb3eee7a))**bigquery:**unit and system test for dataframe with int column with Nan values ([#39](https://www.github.com/googleapis/python-bigquery/issues/39)) ([5fd840e](https://www.github.com/googleapis/python-bigquery/commit/5fd840e9d4c592c4f736f2fd4792c9670ba6795e))

### Bug Fixes

distinguish server timeouts from transport timeouts (

[#43](https://www.github.com/googleapis/python-bigquery/issues/43)) ([a17be5f](https://www.github.com/googleapis/python-bigquery/commit/a17be5f01043f32d9fbfb2ddf456031ea9205c8f))improve cell magic error message on missing query (

[#58](https://www.github.com/googleapis/python-bigquery/issues/58)) ([6182cf4](https://www.github.com/googleapis/python-bigquery/commit/6182cf48aef8f463bb96891cfc44a96768121dbc))**bigquery:**fix start index with page size for list rows ([#27](https://www.github.com/googleapis/python-bigquery/issues/27)) ([400673b](https://www.github.com/googleapis/python-bigquery/commit/400673b5d0f2a6a3d828fdaad9d222ca967ffeff))

## 1.24.0

02-03-2020 01:38 PST

### Implementation Changes

Fix inserting missing repeated fields. (

[#10196](https://github.com/googleapis/google-cloud-python/pull/10196))Deprecate

`client.dataset()`

in favor of`DatasetReference`

. ([#7753](https://github.com/googleapis/google-cloud-python/pull/7753))Use faster

`to_arrow`

+`to_pandas`

in`to_dataframe()`

when`pyarrow`

is available. ([#10027](https://github.com/googleapis/google-cloud-python/pull/10027))Write pandas

`datetime[ns]`

columns to BigQuery TIMESTAMP columns. ([#10028](https://github.com/googleapis/google-cloud-python/pull/10028))

### New Features

Check

`rows`

argument type in`insert_rows()`

. ([#10174](https://github.com/googleapis/google-cloud-python/pull/10174))Check

`json_rows`

arg type in`insert_rows_json()`

. ([#10162](https://github.com/googleapis/google-cloud-python/pull/10162))Make

`RowIterator.to_dataframe_iterable()`

method public. ([#10017](https://github.com/googleapis/google-cloud-python/pull/10017))Add retry parameter to public methods where missing. (

[#10026](https://github.com/googleapis/google-cloud-python/pull/10026))Add timeout parameter to Client and Job public methods. (

[#10002](https://github.com/googleapis/google-cloud-python/pull/10002))Add timeout parameter to

`QueryJob.done()`

method. ([#9875](https://github.com/googleapis/google-cloud-python/pull/9875))Add

`create_bqstorage_client`

parameter to`to_dataframe()`

and`to_arrow()`

methods. ([#9573](https://github.com/googleapis/google-cloud-python/pull/9573))

### Dependencies

- Fix minimum versions of
`google-cloud-core`

and`google-resumable-media`

dependencies. ([#10016](https://github.com/googleapis/google-cloud-python/pull/10016))

### Documentation

Fix a comment typo in

`job.py`

. ([#10209](https://github.com/googleapis/google-cloud-python/pull/10209))Update code samples of load table file and load table URI. (

[#10175](https://github.com/googleapis/google-cloud-python/pull/10175))Uncomment

`Client`

constructor and imports in samples. ([#10058](https://github.com/googleapis/google-cloud-python/pull/10058))Remove unused query code sample. (

[#10024](https://github.com/googleapis/google-cloud-python/pull/10024))Update code samples to use strings for table and dataset IDs. (

[#9974](https://github.com/googleapis/google-cloud-python/pull/9974))

### Internal / Testing Changes

Bump copyright year to 2020, tweak docstring formatting (via synth).

[#10225](https://github.com/googleapis/google-cloud-python/pull/10225)Add tests for concatenating categorical columns. (

[#10180](https://github.com/googleapis/google-cloud-python/pull/10180))Adjust test assertions to the new default timeout. (

[#10222](https://github.com/googleapis/google-cloud-python/pull/10222))Use Python 3.6 for the nox blacken session (via synth). (

[#10012](https://github.com/googleapis/google-cloud-python/pull/10012))

## 1.23.1

12-16-2019 09:39 PST

### Implementation Changes

Add

`iamMember`

entity type to allowed access classes. ([#9973](https://github.com/googleapis/google-cloud-python/pull/9973))Fix typo in import error message (pandas -> pyarrow). (

[#9955](https://github.com/googleapis/google-cloud-python/pull/9955))

### Dependencies

- Add
`six`

as an explicit dependency. ([#9979](https://github.com/googleapis/google-cloud-python/pull/9979))

### Documentation

- Add sample to read from query destination table. (
[#9964](https://github.com/googleapis/google-cloud-python/pull/9964))

## 1.23.0

12-11-2019 13:31 PST

### New Features

Add

`close()`

method to client for releasing open sockets. ([#9894](https://github.com/googleapis/google-cloud-python/pull/9894))Add support of

`use_avro_logical_types`

for extract jobs. ([#9642](https://github.com/googleapis/google-cloud-python/pull/9642))Add support for hive partitioning options configuration. (

[#9626](https://github.com/googleapis/google-cloud-python/pull/9626))Add description for routine entities. (

[#9785](https://github.com/googleapis/google-cloud-python/pull/9785))

### Documentation

- Update code samples to use strings for table and dataset IDs. (
[#9495](https://github.com/googleapis/google-cloud-python/pull/9495))

### Internal / Testing Changes

Run unit tests with Python 3.8. (

[#9880](https://github.com/googleapis/google-cloud-python/pull/9880))Import

`Mapping`

from`collections.abc`

not from`collections`

. ([#9826](https://github.com/googleapis/google-cloud-python/pull/9826))

## 1.22.0

11-13-2019 12:23 PST

### Implementation Changes

Preserve job config passed to Client methods. (

[#9735](https://github.com/googleapis/google-cloud-python/pull/9735))Use pyarrow fallback for improved schema detection. (

[#9321](https://github.com/googleapis/google-cloud-python/pull/9321))Add TypeError if wrong

`job_config type`

is passed to client job methods. ([#9506](https://github.com/googleapis/google-cloud-python/pull/9506))Fix arrow deprecation warning. (

[#9504](https://github.com/googleapis/google-cloud-python/pull/9504))

### New Features

Add

`--destination_table`

parameter to IPython magic. ([#9599](https://github.com/googleapis/google-cloud-python/pull/9599))Allow passing schema as a sequence of dicts. (

[#9550](https://github.com/googleapis/google-cloud-python/pull/9550))Implement defaultEncryptionConfiguration on datasets. (

[#9489](https://github.com/googleapis/google-cloud-python/pull/9489))Add range partitioning to tables, load jobs, and query jobs. (

[#9477](https://github.com/googleapis/google-cloud-python/pull/9477))

### Dependencies

- Pin
`google-resumable-media`

to includ 0.5.x. ([#9572](https://github.com/googleapis/google-cloud-python/pull/9572))

### Documentation

Fix link anchors in external config docstrings. (

[#9627](https://github.com/googleapis/google-cloud-python/pull/9627))Add python 2 sunset banner to documentation. (

[#9036](https://github.com/googleapis/google-cloud-python/pull/9036))Add table create sample using integer range partitioning. (

[#9478](https://github.com/googleapis/google-cloud-python/pull/9478))Document how to achieve higher write limit and add tests. (

[#9574](https://github.com/googleapis/google-cloud-python/pull/9574))Add code sample for scripting. (

[#9537](https://github.com/googleapis/google-cloud-python/pull/9537))Rewrite docs in Google style, part 2. (

[#9481](https://github.com/googleapis/google-cloud-python/pull/9481))Use multi-regional key path for CMEK in snippets. (

[#9523](https://github.com/googleapis/google-cloud-python/pull/9523))

### Internal / Testing Changes

Fix undelete table system test to use milliseconds in snapshot decorator. (

[#9649](https://github.com/googleapis/google-cloud-python/pull/9649))Format code with latest version of black. (

[#9556](https://github.com/googleapis/google-cloud-python/pull/9556))Remove duplicate test dependencies. (

[#9503](https://github.com/googleapis/google-cloud-python/pull/9503))

## 1.21.0

10-16-2019 10:33 PDT

### New Features

add ability to pass in a table ID instead of a query to the

`%%bigquery`

magic ([#9170](https://github.com/googleapis/google-cloud-python/pull/9170))add support for custom

`QueryJobConfig`

in`BigQuery.cursor.execute`

method ([#9278](https://github.com/googleapis/google-cloud-python/pull/9278))store

`QueryJob`

to destination var on error in`%%bigquery`

magic ([#9245](https://github.com/googleapis/google-cloud-python/pull/9245))add script statistics to job resource (

[#9428](https://github.com/googleapis/google-cloud-python/pull/9428))add support for sheets ranges (

[#9416](https://github.com/googleapis/google-cloud-python/pull/9416))add support for listing jobs by parent job (

[#9225](https://github.com/googleapis/google-cloud-python/pull/9225))expose customer managed encryption key for ML models (

[#9302](https://github.com/googleapis/google-cloud-python/pull/9302))add

`Dataset.default_partition_expiration_ms`

and`Table.require_partition_filter`

properties ([#9464](https://github.com/googleapis/google-cloud-python/pull/9464))

### Dependencies

- restrict version range of
`google-resumable-media`

([#9243](https://github.com/googleapis/google-cloud-python/pull/9243))

### Documentation

document how to load data as JSON string (

[#9231](https://github.com/googleapis/google-cloud-python/pull/9231))standardize comments and formatting in existing code samples (

[#9212](https://github.com/googleapis/google-cloud-python/pull/9212))rewrite docstrings in Google style (

[#9326](https://github.com/googleapis/google-cloud-python/pull/9326))fix incorrect links to REST API in reference docs (

[#9436](https://github.com/googleapis/google-cloud-python/pull/9436))

### Internal / Testing Changes

add code samples to lint check (

[#9277](https://github.com/googleapis/google-cloud-python/pull/9277))update code samples to use strings for table and dataset IDs (

[#9136](https://github.com/googleapis/google-cloud-python/pull/9136))simplify scripting system test to reduce flakiness (

[#9458](https://github.com/googleapis/google-cloud-python/pull/9458))

## 1.20.0

09-13-2019 11:22 PDT

### Implementation Changes

Change default endpoint to bigquery.googleapis.com (

[#9213](https://github.com/googleapis/google-cloud-python/pull/9213))Change the default value of Cursor instances’

`arraysize`

attribute to None ([#9199](https://github.com/googleapis/google-cloud-python/pull/9199))Deprecate automatic schema conversion. (

[#9176](https://github.com/googleapis/google-cloud-python/pull/9176))Fix

`list_rows()`

max results with BQ storage client ([#9178](https://github.com/googleapis/google-cloud-python/pull/9178))

### New Features

Add

`Model.encryption_config`

. (via synth) ([#9214](https://github.com/googleapis/google-cloud-python/pull/9214))Add

`Client.insert_rows_from_dataframe()`

method ([#9162](https://github.com/googleapis/google-cloud-python/pull/9162))Add support for array parameters to

`Cursor.execute()`

. ([#9189](https://github.com/googleapis/google-cloud-python/pull/9189))Add support for project IDs with org prefix to

`Table.from_string()`

factory. ([#9161](https://github.com/googleapis/google-cloud-python/pull/9161))Add

`--max_results`

option to Jupyter magics ([#9169](https://github.com/googleapis/google-cloud-python/pull/9169))Autofetch table schema on load if not provided. (

[#9108](https://github.com/googleapis/google-cloud-python/pull/9108))Add

`max_results`

parameter to`QueryJob.result()`

. ([#9167](https://github.com/googleapis/google-cloud-python/pull/9167))

### Documentation

- Fix doc link. (
[#9200](https://github.com/googleapis/google-cloud-python/pull/9200))

### Internal / Testing Changes

## 1.19.0

09-03-2019 14:33 PDT

### Implementation Changes

Raise when unexpected fields are present in the

`LoadJobConfig.schema`

when calling`load_table_from_dataframe`

. ([#9096](https://github.com/googleapis/google-cloud-python/pull/9096))Determine the schema in

`load_table_from_dataframe`

based on dtypes. ([#9049](https://github.com/googleapis/google-cloud-python/pull/9049))Raise helpful error when loading table from dataframe with

`STRUCT`

columns. ([#9053](https://github.com/googleapis/google-cloud-python/pull/9053))Fix schema recognition of struct field types. (

[#9001](https://github.com/googleapis/google-cloud-python/pull/9001))Fix deserializing

`None`

in`QueryJob`

for queries with parameters. ([#9029](https://github.com/googleapis/google-cloud-python/pull/9029))

### New Features

Include indexes in table written by

`load_table_from_dataframe`

, only if fields corresponding to indexes are present in`LoadJobConfig.schema`

. ([#9084](https://github.com/googleapis/google-cloud-python/pull/9084))Add

`client_options`

to constructor. ([#8999](https://github.com/googleapis/google-cloud-python/pull/8999))Add

`--dry_run`

option to`%%bigquery`

magic. ([#9067](https://github.com/googleapis/google-cloud-python/pull/9067))Add

`load_table_from_json()`

method to create a table from a list of dictionaries. ([#9076](https://github.com/googleapis/google-cloud-python/pull/9076))Allow subset of schema to be passed into

`load_table_from_dataframe`

. ([#9064](https://github.com/googleapis/google-cloud-python/pull/9064))Add support for unsetting

`LoadJobConfig.schema`

. ([#9077](https://github.com/googleapis/google-cloud-python/pull/9077))Add support to

`Dataset`

for project IDs containing an org prefix. ([#8877](https://github.com/googleapis/google-cloud-python/pull/8877))Add enum with SQL type names allowed to be used in

`SchemaField`

. ([#9040](https://github.com/googleapis/google-cloud-python/pull/9040))

### Documentation

Fix the reference URL for

`Client.create_dataset()`

. ([#9149](https://github.com/googleapis/google-cloud-python/pull/9149))Update code samples to use strings for table names instead of

`client.dataset()`

. ([#9032](https://github.com/googleapis/google-cloud-python/pull/9032))Remove compatability badges from READMEs. (

[#9035](https://github.com/googleapis/google-cloud-python/pull/9035))Fix Pandas DataFrame load example under Python 2.7. (

[#9022](https://github.com/googleapis/google-cloud-python/pull/9022))

### Internal / Testing Changes

Disable failing snippets test for copying CMEK-protected tables. (

[#9156](https://github.com/googleapis/google-cloud-python/pull/9156))Fix BigQuery client unit test assertions (

[#9112](https://github.com/googleapis/google-cloud-python/pull/9112))Replace avro with arrow schemas in

`test_table.py`

([#9056](https://github.com/googleapis/google-cloud-python/pull/9056))

## 1.18.0

08-08-2019 12:28 PDT

### New Features

Add

`bqstorage_client`

param to`QueryJob.to_arrow()`

([#8693](https://github.com/googleapis/google-cloud-python/pull/8693))Include SQL query and job ID in exception messages. (

[#8748](https://github.com/googleapis/google-cloud-python/pull/8748))Allow using TableListItem to construct a Table object. (

[#8738](https://github.com/googleapis/google-cloud-python/pull/8738))Add StandardSqlDataTypes enum to BigQuery (

[#8782](https://github.com/googleapis/google-cloud-python/pull/8782))Add

`to_standard_sql()`

method to SchemaField ([#8880](https://github.com/googleapis/google-cloud-python/pull/8880))Add debug logging statements to track when BQ Storage API is used. (

[#8838](https://github.com/googleapis/google-cloud-python/pull/8838))Hide error traceback in BigQuery cell magic (

[#8808](https://github.com/googleapis/google-cloud-python/pull/8808))Allow choice of compression when loading from dataframe (

[#8938](https://github.com/googleapis/google-cloud-python/pull/8938))Additional clustering metrics for BQML K-means models (via synth). (

[#8945](https://github.com/googleapis/google-cloud-python/pull/8945))

### Documentation

Add compatibility check badges to READMEs. (

[#8288](https://github.com/googleapis/google-cloud-python/pull/8288))Link to googleapis.dev documentation in READMEs. (

[#8705](https://github.com/googleapis/google-cloud-python/pull/8705))Remove redundant service account key code sample. (

[#8891](https://github.com/googleapis/google-cloud-python/pull/8891))

### Internal / Testing Changes

Fix several pytest “skip if” markers (

[#8694](https://github.com/googleapis/google-cloud-python/pull/8694))Update tests to support conversion of NaN as NULL in pyarrow

`0.14.\*`

. ([#8785](https://github.com/googleapis/google-cloud-python/pull/8785))Mock external calls in one of BigQuery unit tests (

[#8727](https://github.com/googleapis/google-cloud-python/pull/8727))Set IPython user agent when running queries with IPython cell magic (

[#8713](https://github.com/googleapis/google-cloud-python/pull/8713))Use configurable bucket name for GCS samples data in systems tests. (

[#8783](https://github.com/googleapis/google-cloud-python/pull/8783))Move

`maybe_fail_import()`

to top level test utils ([#8840](https://github.com/googleapis/google-cloud-python/pull/8840))Set BQ Storage client user-agent when in Jupyter cell (

[#8734](https://github.com/googleapis/google-cloud-python/pull/8734))

## 1.17.0

07-12-2019 07:56 PDT

### New Features

Support faster Arrow data format in

`to_dataframe`

when using BigQuery Storage API. ([#8551](https://github.com/googleapis/google-cloud-python/pull/8551))Add

`to_arrow`

to get a`pyarrow.Table`

from query results. ([#8609](https://github.com/googleapis/google-cloud-python/pull/8609))

### Dependencies

- Exclude bad 0.14.0
`pyarrow`

release. ([#8551](https://github.com/googleapis/google-cloud-python/pull/8551))

## 1.16.0

07-01-2019 10:22 PDT

### New Features

Add Routines API. (

[#8491](https://github.com/googleapis/google-cloud-python/pull/8491))Add more stats to Models API, such as

`optimization_strategy`

(via synth). ([#8344](https://github.com/googleapis/google-cloud-python/pull/8344))

### Documentation

Add docs job to publish to googleapis.dev. (

[#8464](https://github.com/googleapis/google-cloud-python/pull/8464))Add sample demonstrating how to create a job. (

[#8422](https://github.com/googleapis/google-cloud-python/pull/8422))

### Internal / Testing Changes

- Refactor
`to_dataframe`

to deterministicly update progress bar. ([#8303](https://github.com/googleapis/google-cloud-python/pull/8303))

## 1.15.0

06-14-2019 10:10 PDT

### Implementation Changes

- Fix bug where
`load_table_from_dataframe`

could not append to REQUIRED fields. ([#8230](https://github.com/googleapis/google-cloud-python/pull/8230))

### New Features

- Add
`page_size`

parameter to`QueryJob.result`

. ([#8206](https://github.com/googleapis/google-cloud-python/pull/8206))

## 1.14.0

06-04-2019 11:11 PDT

### New Features

- Add
`maximum_bytes_billed`

argument and`context.default_query_job_config`

property to magics. ([#8179](https://github.com/googleapis/google-cloud-python/pull/8179))

### Dependencies

- Don’t pin
`google-api-core`

in libs using`google-cloud-core`

. ([#8213](https://github.com/googleapis/google-cloud-python/pull/8213))

## 1.13.0

05-31-2019 10:22 PDT

### New Features

- Use
`job_config.schema`

for data type conversion if specified in`load_table_from_dataframe`

. ([#8105](https://github.com/googleapis/google-cloud-python/pull/8105))

### Internal / Testing Changes

Adds private

`_connection`

object to magics context. ([#8192](https://github.com/googleapis/google-cloud-python/pull/8192))Fix coverage in ‘types.py’ (via synth). (

[#8146](https://github.com/googleapis/google-cloud-python/pull/8146))

## 1.12.1

05-21-2019 11:16 PDT

### Implementation Changes

- Don’t raise error when encountering unknown fields in Models API. (
[#8083](https://github.com/googleapis/google-cloud-python/pull/8083))

### Documentation

- Use alabaster theme everwhere. (
[#8021](https://github.com/googleapis/google-cloud-python/pull/8021))

### Internal / Testing Changes

- Add empty lines (via synth). (
[#8049](https://github.com/googleapis/google-cloud-python/pull/8049))

## 1.12.0

05-16-2019 11:25 PDT

### Implementation Changes

Remove duplicates from index on pandas DataFrames returned by

`to_dataframe()`

. ([#7953](https://github.com/googleapis/google-cloud-python/pull/7953))Prevent error when time partitioning is populated with empty dict (

[#7904](https://github.com/googleapis/google-cloud-python/pull/7904))Preserve order in

`to_dataframe`

with BQ Storage from queries containing`ORDER BY`

([#7793](https://github.com/googleapis/google-cloud-python/pull/7793))Respect

`progress_bar_type`

in`to_dataframe`

when used with BQ Storage API ([#7697](https://github.com/googleapis/google-cloud-python/pull/7697))Refactor QueryJob.query to read from resource dictionary (

[#7763](https://github.com/googleapis/google-cloud-python/pull/7763))Close the

`to_dataframe`

progress bar when finished. ([#7757](https://github.com/googleapis/google-cloud-python/pull/7757))Ensure that

`KeyboardInterrupt`

during`to_dataframe`

no longer hangs. ([#7698](https://github.com/googleapis/google-cloud-python/pull/7698))Raise ValueError when BQ Storage is required but missing (

[#7726](https://github.com/googleapis/google-cloud-python/pull/7726))Make

`total_rows`

available on RowIterator before iteration ([#7622](https://github.com/googleapis/google-cloud-python/pull/7622))Avoid masking auth errors in

`to_dataframe`

with BQ Storage API ([#7674](https://github.com/googleapis/google-cloud-python/pull/7674))

### New Features

Phase 1 for storing schemas for later use. (

[#7761](https://github.com/googleapis/google-cloud-python/pull/7761))Add

`destination`

and related properties to LoadJob. ([#7710](https://github.com/googleapis/google-cloud-python/pull/7710))Add

`clustering_fields`

property to TableListItem ([#7692](https://github.com/googleapis/google-cloud-python/pull/7692))Add

`created`

and`expires`

properties to TableListItem ([#7684](https://github.com/googleapis/google-cloud-python/pull/7684))

### Dependencies

Pin

`google-cloud-core >= 1.0.0, < 2.0dev`

. ([#7993](https://github.com/googleapis/google-cloud-python/pull/7993))Add

`[all]`

extras to install all extra dependencies ([#7610](https://github.com/googleapis/google-cloud-python/pull/7610))

### Documentation

- Move table and dataset snippets to samples/ directory (
[#7683](https://github.com/googleapis/google-cloud-python/pull/7683))

### Internal / Testing Changes

Blacken unit tests. (

[#7960](https://github.com/googleapis/google-cloud-python/pull/7960))Cleanup client tests with method to create minimal table resource (

[#7802](https://github.com/googleapis/google-cloud-python/pull/7802))

## 1.11.2

04-05-2019 08:16 PDT

### Dependencies

- Add dependency on protobuf. (
[#7668](https://github.com/googleapis/google-cloud-python/pull/7668))

## 1.11.1

04-04-2019 09:19 PDT

### Internal / Testing Changes

- Increment version number in
`setup.py`

.

## 1.11.0

04-03-2019 19:33 PDT

### Implementation Changes

- Remove classifier for Python 3.4 for end-of-life. (
[#7535](https://github.com/googleapis/google-cloud-python/pull/7535))

### New Features

Enable fastparquet support by using temporary file in

`load_table_from_dataframe`

([#7545](https://github.com/googleapis/google-cloud-python/pull/7545))Allow string for copy sources, query destination, and default dataset (

[#7560](https://github.com/googleapis/google-cloud-python/pull/7560))Add

`progress_bar_type`

argument to`to_dataframe`

to use`tqdm`

to display a progress bar ([#7552](https://github.com/googleapis/google-cloud-python/pull/7552))Call

`get_table`

in`list_rows`

if the schema is not available ([#7621](https://github.com/googleapis/google-cloud-python/pull/7621))Fallback to BQ API when there are problems reading from BQ Storage. (

[#7633](https://github.com/googleapis/google-cloud-python/pull/7633))Add methods for Models API (

[#7562](https://github.com/googleapis/google-cloud-python/pull/7562))Add option to use BigQuery Storage API from IPython magics (

[#7640](https://github.com/googleapis/google-cloud-python/pull/7640))

### Documentation

Remove typo in

`Table.from_api_repr`

docstring. ([#7509](https://github.com/googleapis/google-cloud-python/pull/7509))Add docs session to nox configuration for BigQuery (

[#7541](https://github.com/googleapis/google-cloud-python/pull/7541))

### Internal / Testing Changes

Refactor

`table()`

methods into shared implementation. ([#7516](https://github.com/googleapis/google-cloud-python/pull/7516))Blacken noxfile and setup file in nox session (

[#7619](https://github.com/googleapis/google-cloud-python/pull/7619))Actually use the

`progress_bar_type`

argument in`QueryJob.to_dataframe()`

. ([#7616](https://github.com/googleapis/google-cloud-python/pull/7616))

## 1.10.0

03-06-2019 15:20 PST

### Implementation Changes

Harden ‘ArrayQueryParameter.from_api_repr’ against missing ‘parameterValue’. (

[#7311](https://github.com/googleapis/google-cloud-python/pull/7311))Allow nested records w/ null values. (

[#7297](https://github.com/googleapis/google-cloud-python/pull/7297))

### New Features

Add

`exists_ok`

and`not_found_ok`

options to ignore errors when creating/deleting datasets/tables. ([#7491](https://github.com/googleapis/google-cloud-python/pull/7491))Accept a string in Table and Dataset constructors. (

[#7483](https://github.com/googleapis/google-cloud-python/pull/7483))

### Documentation

Update docstring of RowIterator’s to_dataframe (

[#7306](https://github.com/googleapis/google-cloud-python/pull/7306))Updated client library documentation URLs. (

[#7307](https://github.com/googleapis/google-cloud-python/pull/7307))

### Internal / Testing Changes

- Fix lint. (
[#7383](https://github.com/googleapis/google-cloud-python/pull/7383))

## 1.9.0

02-04-2019 13:28 PST

### New Features

- Add arguments to select
`dtypes`

and use BQ Storage API to`QueryJob.to_dataframe()`

. ([#7241](https://github.com/googleapis/google-cloud-python/pull/7241))

### Documentation

- Add sample for fetching
`total_rows`

from query results. ([#7217](https://github.com/googleapis/google-cloud-python/pull/7217))

## 1.8.1

12-17-2018 17:53 PST

### Documentation

Document Python 2 deprecation (

[#6910](https://github.com/googleapis/google-cloud-python/pull/6910))Normalize docs for ‘page_size’ / ‘max_results’ / ‘page_token’ (

[#6842](https://github.com/googleapis/google-cloud-python/pull/6842))

## 1.8.0

12-10-2018 12:39 PST

### Implementation Changes

Add option to use BQ Storage API with

`to_dataframe`

([#6854](https://github.com/googleapis/google-cloud-python/pull/6854))Fix exception type in comment (

[#6847](https://github.com/googleapis/google-cloud-python/pull/6847))Add

`to_bqstorage`

to convert from Table[Reference] google-cloud-bigquery-storage reference ([#6840](https://github.com/googleapis/google-cloud-python/pull/6840))Import

`iam.policy`

from`google.api_core`

. ([#6741](https://github.com/googleapis/google-cloud-python/pull/6741))Add avro logical type control for load jobs. (

[#6827](https://github.com/googleapis/google-cloud-python/pull/6827))Allow setting partition expiration to ‘None’. (

[#6823](https://github.com/googleapis/google-cloud-python/pull/6823))Add

`retry`

argument to`_AsyncJob.result`

. ([#6302](https://github.com/googleapis/google-cloud-python/pull/6302))

### Dependencies

- Update dependency to google-cloud-core (
[#6835](https://github.com/googleapis/google-cloud-python/pull/6835))

### Documentation

- Add avro load samples (
[#6832](https://github.com/googleapis/google-cloud-python/pull/6832))

### Internal / Testing Changes

## 1.7.0

11-05-2018 16:41 PST

### Implementation Changes

Add destination table properties to

`LoadJobConfig`

. ([#6202](https://github.com/googleapis/google-cloud-python/pull/6202))Allow strings or references in

`create_dataset`

and`create_table`

([#6199](https://github.com/googleapis/google-cloud-python/pull/6199))Fix swallowed error message (

[#6168](https://github.com/googleapis/google-cloud-python/pull/6168))

### New Features

Add

`--params option`

to`%%bigquery`

magic ([#6277](https://github.com/googleapis/google-cloud-python/pull/6277))Expose

`to_api_repr`

method for jobs. ([#6176](https://github.com/googleapis/google-cloud-python/pull/6176))Allow string in addition to DatasetReference / TableReference in Client methods. (

[#6164](https://github.com/googleapis/google-cloud-python/pull/6164))Add keyword arguments to job config constructors for setting properties (

[#6397](https://github.com/googleapis/google-cloud-python/pull/6397))

### Documentation

Update README service links in quickstart guides. (

[#6322](https://github.com/googleapis/google-cloud-python/pull/6322))Move usage guides to their own docs. (

[#6238](https://github.com/googleapis/google-cloud-python/pull/6238))Normalize use of support level badges (

[#6159](https://github.com/googleapis/google-cloud-python/pull/6159))

### Internal / Testing Changes

Deprecation cleanups (

[#6304](https://github.com/googleapis/google-cloud-python/pull/6304))Use

`_get_sub_prop`

helper so missing load stats don’t raise. ([#6269](https://github.com/googleapis/google-cloud-python/pull/6269))Use new Nox (

[#6175](https://github.com/googleapis/google-cloud-python/pull/6175))Harden snippets against transient GCS errors. (

[#6184](https://github.com/googleapis/google-cloud-python/pull/6184))

## 1.6.0

### New Features

### Documentation

- Remove unused “append” samples (
[#6100](https://github.com/googleapis/google-cloud-python/pull/6100))

### Internal / Testing Changes

Address dataset leaks, conflicts in systests (

[#6099](https://github.com/googleapis/google-cloud-python/pull/6099))Harden bucket teardown against

`429 Too Many Requests`

. ([#6101](https://github.com/googleapis/google-cloud-python/pull/6101))

## 1.5.1

### Implementation Changes

Retry ‘502 Bad Gateway’ errors by default. (#5930)

Avoid pulling entire result set into memory when constructing dataframe. (#5870)

Add support for retrying unstructured 429 / 500 / 502 responses. (#6011)

Populate the jobReference from the API response. (#6044)


### Documentation

Prepare documentation for repo split (#5955)

Fix leakage of bigquery/spanner sections into sidebar menu. (#5986)


### Internal / Testing Changes

Test pandas support under Python 3.7. (#5857)

Nox: use inplace installs (#5865)

Update system test to use test data in bigquery-public-data. (#5965)


## 1.5.0

### Implementation Changes

- Make ‘Table.location’ read-only. (#5687)

### New Features

Add ‘clustering_fields’ properties. (#5630)

Add support for job labels (#5654)

Add ‘QueryJob.estimated_bytes_processed’ property (#5655)

Add support/tests for loading tables from ‘gzip.GzipFile’. (#5711)

Add ‘ExternalSourceFormat’ enum. (#5674)

Add default location to client (#5678)


### Documentation

- Fix typo in CopyJob sources docstring (#5690)

### Internal / Testing Changes

Add/refactor snippets for managing BigQuery jobs (#5631)

Reenable systests for ‘dataset.update’/’table.update’. (#5732)


## 1.4.0

### Implementation Changes

Add ‘internalError’ to retryable error reasons. (#5599)

Don’t raise exception if viewing CREATE VIEW DDL results (#5602)


### New Features

Add Orc source format support and samples (#5500)

Move ‘DEFAULT_RETRY’ (w/ its predicate) to a new public ‘retry’ module. (#5552)

Allow listing rows on an empty table. (#5584)


### Documentation

Add load_table_from_dataframe() to usage docs and changelog and dedents snippets in usage page (#5501)

Add samples for query external data sources (GCS & Sheets) (#5491)

Add BigQuery authorized view samples (#5515)

Update docs to show pyarrow as the only dependency of load_table_from_dataframe() (#5582)


### Internal / Testing Changes

Add missing explict coverage for ‘_helpers’ (#5550)

Skip update_table and update_dataset tests until etag issue is resolved. (#5590)


## 1.3.0

### New Features

NUMERIC type support (#5331)

Add timeline and top-level slot-millis to query statistics. (#5312)

Add additional statistics to query plan stages. (#5307)

Add

`client.load_table_from_dataframe()`

(#5387)

### Documentation

Use autosummary to split up API reference docs (#5340)

Fix typo in Client docstrings (#5342)


### Internal / Testing Changes

Prune systests identified as reduntant to snippets. (#5365)

Modify system tests to use prerelease versions of grpcio (#5304)

Improve system test performance (#5319)


## 1.2.0

### Implementation Changes

Switch

`list_partitions`

helper to a direct metatable read (#5273)Fix typo in

`Encoding.ISO_8859_1`

enum value (#5211)

### New Features

Add UnknownJob type for redacted jobs. (#5281)

Add project parameter to

`list_datasets`

and`list_jobs`

(#5217)Add from_string factory methods to Dataset and Table (#5255)

Add column based time partitioning (#5267)


### Documentation

Standardize docstrings for constants (#5289)

Fix docstring / impl of

`ExtractJob.destination_uri_file_counts`

. (#5245)

### Internal / Testing Changes

- Add testing support for Python 3.7; remove testing support for Python 3.4. (#5295)

## 1.1.0

### New Features

- Add
`client.get_service_account_email`

(#5203)

### Documentation

- Update samples and standardize region tags (#5195)

### Internal / Testing Changes

Fix trove classifier to be Production/Stable

Don’t suppress ‘dots’ output on test (#5202)


## 1.0.0

### Implementation Changes

- Remove deprecated Client methods (#5182)

## 0.32.0

### ⚠️ Interface changes

- Use
`job.configuration`

resource for XXXJobConfig classes (#5036)

### Interface additions

Add

`page_size`

parameter for`list_rows`

and use in DB-API for`arraysize`

(#4931)Add IPython magics for running queries (#4983)


### Documentation

- Add job string constant parameters in init and snippets documentation (#4987)

### Internal / Testing changes

Specify IPython version 5.5 when running Python 2.7 tests (#5145)

Move all Dataset property conversion logic into properties (#5130)

Remove unnecessary _Table class from test_job.py (#5126)

Use explicit bytes to initialize ‘BytesIO’. (#5116)

Make SchemaField be able to include description via from_api_repr method (#5114)

Remove _ApiResourceProperty class (#5107)

Add dev version for 0.32.0 release (#5105)

StringIO to BytesIO (#5101)

Shorten snippets test name (#5091)

Don’t use

`selected_fields`

for listing query result rows (#5072)Add location property to job classes. (#5071)

Use autospec for Connection in tests. (#5066)

Add Parquet SourceFormat and samples (#5057)

Remove test_load_table_from_uri_w_autodetect_schema_then_get_job because of duplicate test in snippets (#5004)

Fix encoding variable and strings UTF-8 and ISO-8859-1 difference documentation (#4990)


## 0.31.0

### Interface additions

- Add support for
`EncryptionConfiguration`

(#4845)

### Implementation changes

- Allow listing/getting jobs even when there is an “invalid” job. (#4786)

### Dependencies

- The minimum version for
`google-api-core`

has been updated to version 1.0.0. This may cause some incompatibility with older google-cloud libraries, you will need to update those libraries if you have a dependency conflict. (#4944, #4946)

### Documentation

- Update format in
`Table.full_table_id`

and`TableListItem.full_table_id`

docstrings. (#4906)

### Testing and internal changes

Install local dependencies when running lint (#4936)

Re-enable lint for tests, remove usage of pylint (#4921)

Normalize all setup.py files (#4909)

Remove unnecessary debug print from tests (#4907)

Use constant strings for job properties in tests (#4833)


## 0.30.0

This is the release candidate for v1.0.0.

### Interface changes / additions

- Add
`delete_contents`

to`delete_dataset`

. (#4724)

### Bugfixes

Add handling of missing properties in

`SchemaField.from_api_repr()`

. (#4754)Fix missing return value in

`LoadJobConfig.from_api_repr`

. (#4727)

### Documentation

- Minor documentation and typo fixes. (#4782, #4718, #4784, #4835, #4836)

## 0.29.0

### Interface changes / additions

Add

`to_dataframe()`

method to row iterators. When Pandas is installed this method returns a`DataFrame`

containing the query’s or table’s rows. ([#4354](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4354))Iterate over a

`QueryJob`

to wait for and get the query results. ([#4350](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4350))Add

`Table.reference`

and`Dataset.reference`

properties to get the`TableReference`

or`DatasetReference`

corresponding to that`Table`

or`Dataset`

, respectively. ([#4405](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4405))Add

`Row.keys()`

,`Row.items()`

, and`Row.get()`

. This makes`Row`

act more like a built-in dictionary. ([#4393](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4393),[#4413](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4413))

### Interface changes / breaking changes

Add

`Client.insert_rows()`

and`Client.insert_rows_json()`

, deprecate`Client.create_rows()`

and`Client.create_rows_json()`

. ([#4657](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4657))Add

`Client.list_tables`

, deprecate`Client.list_dataset_tables`

. ([#4653](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4653))`Client.list_tables`

returns an iterators of`TableListItem`

. The API only returns a subset of properties of a table when listing. ([#4427](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4427))Remove

`QueryJob.query_results()`

. Use`QueryJob.result()`

instead. ([#4652](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4652))Remove

`Client.query_rows()`

. Use`Client.query()`

instead. ([#4429](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4429))`Client.list_datasets`

returns an iterator of`DatasetListItem`

. The API only returns a subset of properties of a dataset when listing. ([#4439](https://github.com/GoogleCloudPlatform/google-cloud-python/pull/4439))

## 0.28.0

**0.28.0 significantly changes the interface for this package.** For examples
of the differences between 0.28.0 and previous versions, see
[Migrating to the BigQuery Python client library 0.28](https://cloud.google.com/bigquery/docs/python-client-migration).
These changes can be summarized as follows:

Query and view operations default to the standard SQL dialect. (#4192)

Client functions related to

[jobs](https://cloud.google.com/bigquery/docs/jobs-overview), like running queries, immediately start the job.Functions to create, get, update, delete datasets and tables moved to the client class.


### Fixes

Populate timeout parameter correctly for queries (#4209)

Automatically retry idempotent RPCs (#4148, #4178)

Parse timestamps in query parameters using canonical format (#3945)

Parse array parameters that contain a struct type. (#4040)

Support Sub Second Datetimes in row data (#3901, #3915, #3926), h/t @page1


### Interface changes / additions

Support external table configuration (#4182) in query jobs (#4191) and tables (#4193).

New

`Row`

class allows for access by integer index like a tuple, string index like a dictionary, or attribute access like an object. (#4149)Add option for job ID generation with user-supplied prefix (#4198)

Add support for update of dataset access entries (#4197)

Add support for atomic read-modify-write of a dataset using etag (#4052)

Add support for labels to

`Dataset`

(#4026)Add support for labels to

`Table`

(#4207)Add

`Table.streaming_buffer`

property (#4161)Add

`TableReference`

class (#3942)Add

`DatasetReference`

class (#3938, #3942, #3993)Add

`ExtractJob.destination_uri_file_counts`

property. (#3803)Add

`client.create_rows_json()`

to bypass conversions on streaming writes. (#4189)Add

`client.get_job()`

to get arbitrary jobs. (#3804, #4213)Add filter to

`client.list_datasets()`

(#4205)Add

`QueryJob.undeclared_query_parameters`

property. (#3802)Add

`QueryJob.referenced_tables`

property. (#3801)Add new scalar statistics properties to

`QueryJob`

(#3800)Add

`QueryJob.query_plan`

property. (#3799)

### Interface changes / breaking changes

Remove

`client.run_async_query()`

, use`client.query()`

instead. (#4130)Remove

`client.run_sync_query()`

, use`client.query_rows()`

instead. (#4065, #4248)Make

`QueryResults`

read-only. (#4094, #4144)Make

`get_query_results`

private. Return rows for`QueryJob.result()`

(#3883)Move

`\*QueryParameter`

and`UDFResource`

classes to`query`

module (also exposed in`bigquery`

module). (#4156)

#### Changes to tables

Remove

`client`

from`Table`

class (#4159)Remove

`table.exists()`

(#4145)Move

`table.list_parations`

to`client.list_partitions`

(#4146)Move

`table.upload_from_file`

to`client.load_table_from_file`

(#4136)Move

`table.update()`

and`table.patch()`

to`client.update_table()`

(#4076)Move

`table.insert_data()`

to`client.create_rows()`

. Automatically generates row IDs if not supplied. (#4151, #4173)Move

`table.fetch_data()`

to`client.list_rows()`

(#4119, #4143)Move

`table.delete()`

to`client.delete_table()`

(#4066)Move

`table.create()`

to`client.create_table()`

(#4038, #4043)Move

`table.reload()`

to`client.get_table()`

(#4004)Rename

`Table.name`

attribute to`Table.table_id`

(#3959)`Table`

constructor takes a`TableReference`

as parameter (#3997)

#### Changes to datasets

Remove

`client`

from`Dataset`

class (#4018)Remove

`dataset.exists()`

(#3996)Move

`dataset.list_tables()`

to`client.list_dataset_tables()`

(#4013)Move

`dataset.delete()`

to`client.delete_dataset()`

(#4012)Move

`dataset.patch()`

and`dataset.update()`

to`client.update_dataset()`

(#4003)Move

`dataset.create()`

to`client.create_dataset()`

(#3982)Move

`dataset.reload()`

to`client.get_dataset()`

(#3973)Rename

`Dataset.name`

attribute to`Dataset.dataset_id`

(#3955)`client.dataset()`

returns a`DatasetReference`

instead of`Dataset`

. (#3944)Rename class:

`dataset.AccessGrant -> dataset.AccessEntry`

. (#3798)`dataset.table()`

returns a`TableReference`

instead of a`Table`

(#4014)`Dataset`

constructor takes a DatasetReference (#4036)

#### Changes to jobs

Make

`job.begin()`

method private. (#4242)Add

`LoadJobConfig`

class and modify`LoadJob`

(#4103, #4137)Add

`CopyJobConfig`

class and modify`CopyJob`

(#4051, #4059)Type of Job’s and Query’s

`default_dataset`

changed from`Dataset`

to`DatasetReference`

(#4037)Rename

`client.load_table_from_storage()`

to`client.load_table_from_uri()`

(#4235)Rename

`client.extract_table_to_storage`

to`client.extract_table()`

. Method starts the extract job immediately. (#3991, #4177)Rename

`XJob.name`

to`XJob.job_id`

. (#3962)Rename job classes.

`LoadTableFromStorageJob -> LoadJob`

and`ExtractTableToStorageJob -> jobs.ExtractJob`

(#3797)

### Dependencies

- Updating to
`google-cloud-core ~= 0.28`

, in particular, the`google-api-core`

package has been moved out of`google-cloud-core`

. (#4221)

PyPI: [https://pypi.org/project/google-cloud-bigquery/0.28.0/](https://pypi.org/project/google-cloud-bigquery/0.28.0/)

## 0.27.0

Remove client-side enum validation. (#3735)

Add

`Table.row_from_mapping`

helper. (#3425)Move

`google.cloud.future`

to`google.api.core`

(#3764)Fix

`__eq__`

and`__ne__`

. (#3765)Move

`google.cloud.iterator`

to`google.api.core.page_iterator`

(#3770)`nullMarker`

support for BigQuery Load Jobs (#3777), h/t @leondealmeidaAllow

`job_id`

to be explicitly specified in DB-API. (#3779)Add support for a custom null marker. (#3776)

Add

`SchemaField`

serialization and deserialization. (#3786)Add

`get_query_results`

method to the client. (#3838)Poll for query completion via

`getQueryResults`

method. (#3844)Allow fetching more than the first page when

`max_results`

is set. (#3845)

PyPI: [https://pypi.org/project/google-cloud-bigquery/0.27.0/](https://pypi.org/project/google-cloud-bigquery/0.27.0/)

## 0.26.0

### Notable implementation changes

- Using the
`requests`

transport attached to a Client for for resumable media (i.e. downloads and uploads) (#3705) (this relates to the`httplib2`

to`requests`

switch)

### Interface changes / additions

Adding

`autodetect`

property on`LoadTableFromStorageJob`

to enable schema autodetection. (#3648)Implementing the Python Futures interface for Jobs. Call

`job.result()`

to wait for jobs to complete instead of polling manually on the job status. (#3626)Adding

`is_nullable`

property on`SchemaField`

. Can be used to check if a column is nullable. (#3620)`job_name`

argument added to`Table.upload_from_file`

for setting the job ID. (#3605)Adding

`google.cloud.bigquery.dbapi`

package, which implements PEP-249 DB-API specification. (#2921)Adding

`Table.view_use_legacy_sql`

property. Can be used to create views with legacy or standard SQL. (#3514)

### Interface changes / breaking changes

Removing

`results()`

method from the`QueryJob`

class. Use`query_results()`

instead. (#3661)`SchemaField`

is now immutable. It is also hashable so that it can be used in sets. (#3601)

### Dependencies

Updating to

`google-cloud-core ~= 0.26`

, in particular, the underlying HTTP transport switched from`httplib2`

to`requests`

(#3654, #3674)Adding dependency on

`google-resumable-media`

for loading BigQuery tables from local files. (#3555)

### Packaging

Fix inclusion of

`tests`

(vs.`unit_tests`

) in`MANIFEST.in`

(#3552)Updating

`author_email`

in`setup.py`

to`googleapis-publisher@google.com`

. (#3598)

PyPI: [https://pypi.org/project/google-cloud-bigquery/0.26.0/](https://pypi.org/project/google-cloud-bigquery/0.26.0/)