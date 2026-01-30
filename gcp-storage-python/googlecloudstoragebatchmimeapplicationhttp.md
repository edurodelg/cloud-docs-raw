---
source_url: https://cloud.google.com/python/docs/reference/storage/latest/google.cloud.storage.batch.MIMEApplicationHTTP
fetched_at: 2026-01-30T23:53:02.436269
---

# Class MIMEApplicationHTTP (3.8.0)

`MIMEApplicationHTTP(method, uri, headers, body)`


MIME type for `application/http`

.

Constructs payload from headers and body

## Parameters |
|
|---|---|
Name |
Description |
`method` |
`str`
HTTP method |
`uri` |
`str`
URI for HTTP request |
`headers` |
`dict`
HTTP headers |
`body` |
`str`
(Optional) HTTP payload |

## Methods

### MIMEApplicationHTTP

`MIMEApplicationHTTP(method, uri, headers, body)`


Create an application/* type MIME document.

_data contains the bytes for the raw application data.

_subtype is the MIME content type subtype, defaulting to 'octet-stream'.

_encoder is a function which will perform the actual encoding for transport of the application data, defaulting to base64 encoding.

Any additional keyword arguments are passed to the base class constructor, which turns them into parameters on the Content-Type header.