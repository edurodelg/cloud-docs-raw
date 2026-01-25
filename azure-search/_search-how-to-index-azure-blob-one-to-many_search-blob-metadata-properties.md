---
merged_at: 2026-01-25T03:18:13.784145
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-azure-blob-one-to-many.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-azure-blob-one-to-many -->

# Indexing blobs and files to produce multiple search documents

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to**: [Blob indexers](search-how-to-index-azure-blob-storage), [File indexers](search-file-storage-integration)

By default, an indexer treats the contents of a blob or file as a single search document. If you want a more granular representation in a search index, you can set **parsingMode** values to create multiple search documents from one blob or file. The **parsingMode** values that result in many search documents include `delimitedText`

(for [CSV](search-how-to-index-azure-blob-csv)), `jsonArray`

or `jsonLines`

(for [JSON](search-how-to-index-azure-blob-json)), or `markdown`

with sub-mode `oneToMany`

for [markdown](search-how-to-index-azure-blob-markdown).

When you use any of these parsing modes, the new search documents that emerge must have unique document keys, and a problem arises in determining where that value comes from. The parent blob has at least one unique value in the form of `metadata_storage_path property`

, but if it contributes that value to more than one search document, the key is no longer unique in the index.

To address this problem, the blob indexer generates an `AzureSearch_DocumentKey`

that uniquely identifies each child search document created from the single blob parent. This article explains how this feature works.

## One-to-many document key

A document key uniquely identifies each document in an index. When no parsing mode is specified, and if there's no [explicit field mapping](search-indexer-field-mappings) in the indexer definition for the search document key, the blob indexer automatically maps the `metadata_storage_path property`

as the document key. This default mapping ensures that each blob appears as a distinct search document. It also eliminates the need for you to manually create this field mapping. Normally, fields with identical names and types are the only ones mapped automatically.

In a one-to-many search document scenario, an implicit document key based on `metadata_storage_path property`

isn't possible. As a workaround, Azure AI Search can generate a document key for each individual entity extracted from a blob. The system generates a key called `AzureSearch_DocumentKey`

and adds it to each search document. The indexer keeps track of the "many documents" created from each blob, and can target updates to the search index when source data changes over time.

By default, when no explicit field mappings for the key index field are specified, the `AzureSearch_DocumentKey`

is mapped to it, using the `base64Encode`

field-mapping function.

## Example

Assume an index definition with the following fields:

`id`

`temperature`

`pressure`

`timestamp`


And your blob container has blobs with the following structure:

*Blob1.json*

```
{ "temperature": 100, "pressure": 100, "timestamp": "2024-02-13T00:00:00Z" }
{ "temperature" : 33, "pressure" : 30, "timestamp": "2024-02-14T00:00:00Z" }
```


*Blob2.json*

```
{ "temperature": 1, "pressure": 1, "timestamp": "2023-01-12T00:00:00Z" }
{ "temperature" : 120, "pressure" : 3, "timestamp": "2022-05-11T00:00:00Z" }
```


When you create an indexer and set the **parsingMode** to `jsonLines`

- without specifying any explicit field mappings for the key field, the following mapping is applied implicitly.

```
{
"sourceFieldName" : "AzureSearch_DocumentKey",
"targetFieldName": "id",
"mappingFunction": { "name" : "base64Encode" }
}
```


This setup results in disambiguated document keys, similar to the following illustration (base64-encoded ID shortened for brevity).

| ID | temperature | pressure | timestamp |
|---|---|---|---|
| aHR0 ... YjEuanNvbjsx | 100 | 100 | 2024-02-13T00:00:00Z |
| aHR0 ... YjEuanNvbjsy | 33 | 30 | 2024-02-14T00:00:00Z |
| aHR0 ... YjIuanNvbjsx | 1 | 1 | 2023-01-12T00:00:00Z |
| aHR0 ... YjIuanNvbjsy | 120 | 3 | 2022-05-11T00:00:00Z |

## Custom field mapping for index key field

Assuming the same index definition as the previous example, suppose your blob container has blobs with the following structure:

*Blob1.json*

```
recordid, temperature, pressure, timestamp
1, 100, 100,"2024-02-13T00:00:00Z"
2, 33, 30,"2024-02-14T00:00:00Z"
```


*Blob2.json*

```
recordid, temperature, pressure, timestamp
1, 1, 1,"20123-01-12T00:00:00Z"
2, 120, 3,"2022-05-11T00:00:00Z"
```


When you create an indexer with `delimitedText`

**parsingMode**, it might feel natural to set up a field-mapping function to the key field as follows:

```
{
"sourceFieldName" : "recordid",
"targetFieldName": "id"
}
```


However, this mapping doesn't result in four documents showing up in the index because the `recordid`

field isn't unique *across blobs*. Hence, we recommend you to make use of the implicit field mapping applied from the `AzureSearch_DocumentKey`

property to the key index field for "one-to-many" parsing modes.

If you do want to set up an explicit field mapping, make sure that the *sourceField* is distinct for each individual entity **across all blobs**.

Note

The approach used by `AzureSearch_DocumentKey`

of ensuring uniqueness per extracted entity is subject to change and therefore you shouldn't rely on its value for your application's needs.

## Specify the index key field in your data

Assuming the same index definition as the previous example and **parsingMode** is set to `jsonLines`

without specifying any explicit field mappings so the mappings look like in the first example, suppose your blob container has blobs with the following structure:

*Blob1.json*

```
id, temperature, pressure, timestamp
1, 100, 100,"2024-02-13T00:00:00Z"
2, 33, 30,"2024-02-14T00:00:00Z"
```


*Blob2.json*

```
id, temperature, pressure, timestamp
1, 1, 1,"2023-01-12T00:00:00Z"
2, 120, 3,"2022-05-11T00:00:00Z"
```


Each document contains the `id`

field, which is defined as the `key`

field in the index. In this situation, the system generates a unique AzureSearch_DocumentKey`for the document, but it isn't used as the "key." Instead, the value of the`

id`field is mapped to the`

key` field.

Similar to the previous example, this mapping doesn't result in four documents showing up in the index because the `id`

field isn't unique *across blobs*. When this situation occurs, any JSON entry that specifies an `id`

causes a merge with the existing document instead of uploading a new one. The index then reflects the latest state of the entry with the specified `id`

.

## Limitations

When a document entry in the index is created from a line in a file, as explained in this article, deleting that line from the file doesn't automatically remove the corresponding entry from the index. To delete the document entry, you must manually submit a deletion request to the index using the [REST API deletion operation](/en-us/rest/api/searchservice/addupdate-or-delete-documents).

## Next steps

If you aren't already familiar with the basic structure and workflow of blob indexing, you should review [Indexing Azure Blob Storage with Azure AI Search](search-how-to-index-azure-blob-json) first. For more information about parsing modes for different blob content types, review the following articles.


---

<!-- DOCUMENTO FUSIONADO: search-blob-metadata-properties.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-blob-metadata-properties -->

# Content metadata properties used in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Several indexer-supported data sources, including Azure Blob Storage, Azure Data Lake Storage Gen2, and SharePoint, contain standalone files or embedded objects of various content types. Many of those content types have metadata properties that can be useful to index. Just as you can create search fields for standard blob properties like `metadata_storage_name`

, you can create fields in a search index for metadata properties that are specific to a document format.

## Supported document formats

Azure AI Search supports blob indexing and SharePoint document indexing for the following document formats:

- CSV (see
[Indexing CSV blobs](search-how-to-index-azure-blob-csv)) - EML
- EPUB
- GZ
- HTML
- JSON (see
[Indexing JSON blobs](search-how-to-index-azure-blob-json)) - KML (XML for geographic representations)
- Markdown
- Microsoft Office formats: DOCX/DOC/DOCM, XLSX/XLS/XLSM, PPTX/PPT/PPTM, MSG (Outlook emails), XML (both 2003 and 2006 WORD XML)
- Open Document formats: ODT, ODS, ODP
- Plain text files (see also
[Indexing plain text](search-how-to-index-azure-blob-plaintext)) - RTF
- XML
- ZIP

## Document format properties

The following table summarizes processing for each document format, and describes the metadata properties extracted by a blob indexer and the SharePoint indexer.

| Document format / content type | Extracted metadata | Processing details |
|---|---|---|
| CSV (text/csv) | `metadata_content_type` `metadata_content_encoding` |
Extract text NOTE: If you need to extract multiple document fields from a CSV blob, see
|
| DOC (application/msword) | `metadata_content_type` `metadata_author` `metadata_character_count` `metadata_creation_date` `metadata_last_modified` `metadata_page_count` `metadata_word_count` |
Extract text, including embedded documents |
| DOCM (application/vnd.ms-word.document.macroenabled.12) | `metadata_content_type` `metadata_author` `metadata_character_count` `metadata_creation_date` `metadata_last_modified` `metadata_page_count` `metadata_word_count` |
Extract text, including embedded documents |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) | `metadata_content_type` `metadata_author` `metadata_character_count` `metadata_creation_date` `metadata_last_modified` `metadata_page_count` `metadata_word_count` |
Extract text, including embedded documents |
| EML (message/rfc822) | `metadata_content_type` `metadata_message_from` `metadata_message_to` `metadata_message_cc` `metadata_creation_date` `metadata_subject` |
Extract text, including attachments |
| EPUB (application/epub+zip) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_title` `metadata_description` `metadata_language` `metadata_keywords` `metadata_identifier` `metadata_publisher` |
Extract text from all documents in the archive |
| GZ (application/gzip) | `metadata_content_type` |
Extract text from all documents in the archive |
| HTML (text/html or application/xhtml+xml) | `metadata_content_encoding` `metadata_content_type` `metadata_language` `metadata_description` `metadata_keywords` `metadata_title` |
Strip HTML elements and extract text |
| JSON (application/json) | `metadata_content_type` `metadata_content_encoding` |
Extract text NOTE: If you need to extract multiple document fields from a JSON blob, see
|
| KML (application/vnd.google-earth.kml+xml) | `metadata_content_type` `metadata_content_encoding` `metadata_language` |
Strip XML elements and extract text |
| MSG (application/vnd.ms-outlook) | `metadata_content_type` `metadata_message_from` `metadata_message_from_email` `metadata_message_to` `metadata_message_to_email` `metadata_message_cc` `metadata_message_cc_email` `metadata_message_bcc` `metadata_message_bcc_email` `metadata_creation_date` `metadata_last_modified` `metadata_subject` |
Extract text, including text extracted from attachments. `metadata_message_to_email` , `metadata_message_cc_email` , and `metadata_message_bcc_email` are string collections. The rest of the fields are strings. |
| ODP (application/vnd.oasis.opendocument.presentation) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` `metadata_title` |
Extract text, including embedded documents |
| ODS (application/vnd.oasis.opendocument.spreadsheet) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` |
Extract text, including embedded documents |
| ODT (application/vnd.oasis.opendocument.text) | `metadata_content_type` `metadata_author` `metadata_character_count` `metadata_creation_date` `metadata_last_modified` `metadata_page_count` `metadata_word_count` |
Extract text, including embedded documents |
| PDF (application/pdf) | `metadata_content_type` `metadata_language` `metadata_author` `metadata_title` `metadata_creation_date` |
Extract text, including embedded documents (excluding images) |
| Plain text (text/plain) | `metadata_content_type` `metadata_content_encoding` `metadata_language` |
Extract text |
| PPT (application/vnd.ms-powerpoint) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` `metadata_slide_count` `metadata_title` |
Extract text, including embedded documents |
| PPTM (application/vnd.ms-powerpoint.presentation.macroenabled.12) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` `metadata_slide_count` `metadata_title` |
Extract text, including embedded documents |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` `metadata_slide_count` `metadata_title` |
Extract text, including embedded documents |
| RTF (application/rtf) | `metadata_content_type` `metadata_author` `metadata_character_count` `metadata_creation_date` `metadata_last_modified` `metadata_page_count` `metadata_word_count` |
Extract text |
| WORD 2003 XML (application/vnd.ms-wordml) | `metadata_content_type` `metadata_author` `metadata_creation_date` |
Strip XML elements and extract text |
| WORD XML (application/vnd.ms-word2006ml) | `metadata_content_type` `metadata_author` `metadata_character_count` `metadata_creation_date` `metadata_last_modified` `metadata_page_count` `metadata_word_count` |
Strip XML elements and extract text |
| XLS (application/vnd.ms-excel) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` |
Extract text, including embedded documents |
| XLSM (application/vnd.ms-excel.sheet.macroenabled.12) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` |
Extract text, including embedded documents |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) | `metadata_content_type` `metadata_author` `metadata_creation_date` `metadata_last_modified` |
Extract text, including embedded documents |
| XML (application/xml) | `metadata_content_type` `metadata_content_encoding` `metadata_language` |
Strip XML elements and extract text |
| ZIP (application/zip) | `metadata_content_type` |
Extract text from all documents in the archive |
