---
source_url: https://docs.cloud.google.com/python/docs/reference/bigquery/latest/google.cloud.bigquery.encryption_configuration.EncryptionConfiguration
fetched_at: 2026-01-25T02:06:17.194114
---

# Class EncryptionConfiguration (3.40.0)


      
      Save and categorize content based on your preferences.

`EncryptionConfiguration(kms_key_name=None)`


Custom encryption configuration (e.g., Cloud KMS keys).

## Parameter |
|
|---|---|
Name |
Description |
`kms_key_name` |
`str`
resource ID of Cloud KMS key used for encryption |

## Properties

### kms_key_name

str: Resource ID of Cloud KMS key

Resource ID of Cloud KMS key or :data:`None`

if using default
encryption.

## Methods

### from_api_repr

`from_api_repr(resource)`


Construct an encryption configuration from its API representation

Parameter |
|
|---|---|
Name |
Description |
`resource` |
`Dict[str, object]`
An encryption configuration representation as returned from the API. |

Returns |
|
|---|---|
Type |
Description |
|
An encryption configuration parsed from `resource` . |

### to_api_repr

`to_api_repr()`


Construct the API resource representation of this encryption configuration.

Returns |
|
|---|---|
Type |
Description |
`Dict[str, object]` |
Encryption configuration as represented as an API resource |