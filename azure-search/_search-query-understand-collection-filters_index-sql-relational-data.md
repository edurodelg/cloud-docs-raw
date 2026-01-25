---
merged_at: 2026-01-25T02:11:58.433563
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-understand-collection-filters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-understand-collection-filters -->

# Understand how OData collection filters work in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides background for developers who are writing advanced filters with complex lambda expressions. The article explains why the rules for collection filters exist by exploring how Azure AI Search executes these filters.

When you build a [filter](query-odata-filter-orderby-syntax) on collection fields in Azure AI Search, you can use the [ any and all operators](search-query-odata-collection-operators) together with


**lambda expressions**. Lambda expressions are Boolean expressions that refer to a

**range variable**. In filters that use a lambda expression, the

`any`

and `all`

operators are analogous to a `for`

loop in most programming languages, with the range variable taking the role of loop variable, and the lambda expression as the body of the loop. The range variable takes on the "current" value of the collection during iteration of the loop.At least that's how it works conceptually. In reality, Azure AI Search implements filters in a very different way to how `for`

loops work. Ideally, this difference would be invisible to you, but in certain situations it isn't. The end result is that there are rules you have to follow when writing lambda expressions.

Note

For information on what the rules for collection filters are, including examples, see [Troubleshooting OData collection filters in Azure AI Search](search-query-troubleshoot-collection-filters).

## Why collection filters are limited

There are three underlying reasons why filter features aren't fully supported for all types of collections:

- Only certain operators are supported for certain data types. For example, it doesn't make sense to compare the Boolean values
`true`

and`false`

using`lt`

,`gt`

, and so on. - Azure AI Search doesn't support
*correlated search*on fields of type`Collection(Edm.ComplexType)`

. - Azure AI Search uses inverted indexes to execute filters over all types of data, including collections.

The first reason is just a consequence of how the OData language and EDM type system are defined. The last two are explained in more detail in the rest of this article.

## Correlated versus uncorrelated search

When you apply multiple filter criteria over a collection of complex objects, the criteria are correlated because they apply to *each object in the collection*. For example, the following filter returns hotels that have at least one deluxe room with a rate less than 100:

```
Rooms/any(room: room/Type eq 'Deluxe Room' and room/BaseRate lt 100)
```


If filtering was *uncorrelated*, the above filter might return hotels where one room is deluxe and a different room has a base rate less than 100. That wouldn't make sense, since both clauses of the lambda expression apply to the same range variable, namely `room`

. This is why such filters are correlated.

However, for full-text search, there's no way to refer to a specific range variable. If you use fielded search to issue a [full Lucene query](query-lucene-syntax) like this one:

```
Rooms/Type:deluxe AND Rooms/Description:"city view"
```


you might get hotels back where one room is deluxe, and a different room mentions "city view" in the description. For example, the document below with `Id`

of `1`

would match the query:

```
{
"value": [
{
"Id": "1",
"Rooms": [
{ "Type": "deluxe", "Description": "Large garden view suite" },
{ "Type": "standard", "Description": "Standard city view room" }
]
},
{
"Id": "2",
"Rooms": [
{ "Type": "deluxe", "Description": "Courtyard motel room" }
]
}
]
}
```


The reason is that `Rooms/Type`

refers to all the analyzed terms of the `Rooms/Type`

field in the entire document, and similarly for `Rooms/Description`

, as shown in the tables below.

How `Rooms/Type`

is stored for full-text search:

Term in `Rooms/Type` |
Document IDs |
|---|---|
| deluxe | 1, 2 |
| standard | 1 |

How `Rooms/Description`

is stored for full-text search:

Term in `Rooms/Description` |
Document IDs |
|---|---|
| courtyard | 2 |
| city | 1 |
| garden | 1 |
| large | 1 |
| motel | 2 |
| room | 1, 2 |
| standard | 1 |
| suite | 1 |
| view | 1 |

So unlike the filter above, which basically says "match documents where a room has `Type`

equal to 'Deluxe Room' and **that same room** has `BaseRate`

less than 100", the search query says "match documents where `Rooms/Type`

has the term "deluxe" and `Rooms/Description`

has the phrase "city view". There's no concept of individual rooms whose fields can be correlated in the latter case.

## Inverted indexes and collections

You might have noticed that there are far fewer restrictions on lambda expressions over complex collections than there are for simple collections like `Collection(Edm.Int32)`

, `Collection(Edm.GeographyPoint)`

, and so on. This is because Azure AI Search stores complex collections as actual collections of subdocuments, while simple collections aren't stored as collections at all.

For example, consider a filterable string collection field like `seasons`

in an index for an online retailer. Some documents uploaded to this index might look like this:

```
{
"value": [
{
"id": "1",
"name": "Hiking boots",
"seasons": ["spring", "summer", "fall"]
},
{
"id": "2",
"name": "Rain jacket",
"seasons": ["spring", "fall", "winter"]
},
{
"id": "3",
"name": "Parka",
"seasons": ["winter"]
}
]
}
```


The values of the `seasons`

field are stored in a structure called an **inverted index**, which looks something like this:

| Term | Document IDs |
|---|---|
| spring | 1, 2 |
| summer | 1 |
| fall | 1, 2 |
| winter | 2, 3 |

This data structure is designed to answer one question with great speed: In which documents does a given term appear? Answering this question works more like a plain equality check than a loop over a collection. In fact, this is why for string collections, Azure AI Search only allows `eq`

as a comparison operator inside a lambda expression for `any`

.

Next, we look at how it's possible to combine multiple equality checks on the same range variable with `or`

. It works thanks to algebra and [the distributive property of quantifiers](https://en.wikipedia.org/wiki/Existential_quantification#Negation). This expression:

```
seasons/any(s: s eq 'winter' or s eq 'fall')
```


is equivalent to:

```
seasons/any(s: s eq 'winter') or seasons/any(s: s eq 'fall')
```


and each of the two `any`

sub-expressions can be efficiently executed using the inverted index. Also, thanks to [the negation law of quantifiers](https://en.wikipedia.org/wiki/Existential_quantification#Negation), this expression:

```
seasons/all(s: s ne 'winter' and s ne 'fall')
```


is equivalent to:

```
not seasons/any(s: s eq 'winter' or s eq 'fall')
```


which is why it's possible to use `all`

with `ne`

and `and`

.

Note

Although the details are beyond the scope of this document, these same principles extend to [distance and intersection tests for collections of geo-spatial points](search-query-odata-geo-spatial-functions) as well. This is why, in `any`

:

`geo.intersects`

cannot be negated`geo.distance`

must be compared using`lt`

or`le`

- expressions must be combined with
`or`

, not`and`


The converse rules apply for `all`

.

A wider variety of expressions are allowed when filtering on collections of data types that support the `lt`

, `gt`

, `le`

, and `ge`

operators, such as `Collection(Edm.Int32)`

for example. Specifically, you can use `and`

as well as `or`

in `any`

, as long as the underlying comparison expressions are combined into **range comparisons** using `and`

, which are then further combined using `or`

. This structure of Boolean expressions is called [Disjunctive Normal Form (DNF)](https://en.wikipedia.org/wiki/Disjunctive_normal_form), otherwise known as "ORs of ANDs". Conversely, lambda expressions for `all`

for these data types must be in [Conjunctive Normal Form (CNF)](https://en.wikipedia.org/wiki/Conjunctive_normal_form), otherwise known as "ANDs of ORs". Azure AI Search allows such range comparisons because it can execute them using inverted indexes efficiently, just like it can do fast term lookup for strings.

In summary, here are the rules of thumb for what's allowed in a lambda expression:

- Inside
`any`

,*positive checks*are always allowed, like equality, range comparisons,`geo.intersects`

, or`geo.distance`

compared with`lt`

or`le`

(think of "closeness" as being like equality when it comes to checking distance). - Inside
`any`

,`or`

is always allowed. You can use`and`

only for data types that can express range checks, and only if you use ORs of ANDs (DNF). - Inside
`all`

, the rules are reversed. Only*negative checks*are allowed, you can use`and`

always, and you can use`or`

only for range checks expressed as ANDs of ORs (CNF).

In practice, these are the types of filters you're most likely to use anyway. It's still helpful to understand the boundaries of what's possible though.

For specific examples of which kinds of filters are allowed and which aren't, see [How to write valid collection filters](search-query-troubleshoot-collection-filters#bkmk_examples).


---

<!-- DOCUMENTO FUSIONADO: index-sql-relational-data.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/index-sql-relational-data -->

# How to model relational SQL data for import and indexing in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search accepts a flat rowset as input to the [indexing pipeline](search-what-is-an-index). If your source data originates from joined tables in a SQL Server relational database, this article explains how to construct the rowset, and how to model a parent-child relationship in an Azure AI Search index.

As an illustration, we refer to a hypothetical hotels database, based on [demo data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels). Assume the database consists of a `Hotels$`

table with 50 hotels, and a `Rooms$`

table with rooms of varying types, rates, and amenities, for a total of 750 rooms. There's a one-to-many relationship between the tables. In our approach, a view provides the query that returns 50 rows, one row per hotel, with associated room detail embedded into each row.

## The problem of denormalized data

One of the challenges in working with one-to-many relationships is that standard queries built on joined tables return denormalized data, which doesn't work well in an Azure AI Search scenario. Consider the following example that joins hotels and rooms.

```
SELECT * FROM Hotels$
INNER JOIN Rooms$
ON Rooms$.HotelID = Hotels$.HotelID
```


Results from this query return all of the Hotel fields, followed by all Room fields, with preliminary hotel information repeating for each room value.

While this query succeeds on the surface (providing all of the data in a flat rowset), it fails in delivering the right document structure for the expected search experience. During indexing, Azure AI Search creates one search document for each row ingested. If your search documents looked like the above results, you would have perceived duplicates - seven separate documents for the Old Century Hotel alone. A query on "hotels in Florida" would return seven results for just the Old Century Hotel, pushing other relevant hotels deep into the search results.

To get the expected experience of one document per hotel, you should provide a rowset at the right granularity, but with complete information. This article explains how.

## Define a query that returns embedded JSON

To deliver the expected search experience, your data set should consist of one row for each search document in Azure AI Search. In our example, we want one row for each hotel, but we also want our users to be able to search on other room-related fields they care about, such as the nightly rate, size and number of beds, or a view of the beach, all of which are part of a room detail.

The solution is to capture the room detail as nested JSON, and then insert the JSON structure into a field in a view, as shown in the second step.

Assume you have two joined tables,

`Hotels$`

and`Rooms$`

, that contain details for 50 hotels and 750 rooms and are joined on the HotelID field. Individually, these tables contain 50 hotels and 750 related rooms.`CREATE TABLE [dbo].[Hotels$]( [HotelID] [nchar](10) NOT NULL, [HotelName] [nvarchar](255) NULL, [Description] [nvarchar](max) NULL, [Description_fr] [nvarchar](max) NULL, [Category] [nvarchar](255) NULL, [Tags] [nvarchar](255) NULL, [ParkingIncluded] [float] NULL, [SmokingAllowed] [float] NULL, [LastRenovationDate] [smalldatetime] NULL, [Rating] [float] NULL, [StreetAddress] [nvarchar](255) NULL, [City] [nvarchar](255) NULL, [State] [nvarchar](255) NULL, [ZipCode] [nvarchar](255) NULL, [GeoCoordinates] [nvarchar](255) NULL ) ON [PRIMARY] TEXTIMAGE_ON [PRIMARY] GO CREATE TABLE [dbo].[Rooms$]( [HotelID] [nchar](10) NULL, [Description] [nvarchar](255) NULL, [Description_fr] [nvarchar](255) NULL, [Type] [nvarchar](255) NULL, [BaseRate] [float] NULL, [BedOptions] [nvarchar](255) NULL, [SleepsCount] [float] NULL, [SmokingAllowed] [float] NULL, [Tags] [nvarchar](255) NULL ) ON [PRIMARY] GO`

Create a view composed of all fields in the parent table (

`SELECT * from dbo.Hotels$`

), with the addition of a new*Rooms*field that contains the output of a nested query. A**FOR JSON AUTO**clause on`SELECT * from dbo.Rooms$`

structures the output as JSON.`CREATE VIEW [dbo].[HotelRooms] AS SELECT *, (SELECT * FROM dbo.Rooms$ WHERE dbo.Rooms$.HotelID = dbo.Hotels$.HotelID FOR JSON AUTO) AS Rooms FROM dbo.Hotels$ GO`

The following screenshot shows the resulting view, with the

*Rooms*nvarchar field at the bottom. The*Rooms*field exists only in the HotelRooms view.Run

`SELECT * FROM dbo.HotelRooms`

to retrieve the row set. This query returns 50 rows, one per hotel, with associated room information as a JSON collection.

This rowset is now ready for import into Azure AI Search.

Note

This approach assumes that embedded JSON is under the [maximum column size limits of SQL Server](/en-us/sql/sql-server/maximum-capacity-specifications-for-sql-server).

## Use a complex collection for the "many" side of a one-to-many relationship

On the Azure AI Search side, create an index schema that models the one-to-many relationship using nested JSON. The result set you created in the previous section generally corresponds to the index schema provided next (we cut some fields for brevity).

The following example is similar to the example in [How to model complex data types](search-howto-complex-data-types#create-complex-fields). The *Rooms* structure, which has been the focus of this article, is in the fields collection of an index named *hotels*. This example also shows a complex type for *Address*, which differs from *Rooms* in that it's composed of a fixed set of items, as opposed to the multiple, arbitrary number of items allowed in a collection.

```
{
"name": "hotels",
"fields": [
{ "name": "HotelId", "type": "Edm.String", "key": true, "filterable": true },
{ "name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false },
{ "name": "Description", "type": "Edm.String", "searchable": true, "analyzer": "en.lucene" },
{ "name": "Description_fr", "type": "Edm.String", "searchable": true, "analyzer": "fr.lucene" },
{ "name": "Category", "type": "Edm.String", "searchable": true, "filterable": true, "facetable": true },
{ "name": "ParkingIncluded", "type": "Edm.Boolean", "filterable": true, "facetable": true },
{ "name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "facetable": true },
{ "name": "Address", "type": "Edm.ComplexType",
"fields": [
{ "name": "StreetAddress", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "searchable": true },
{ "name": "City", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true },
{ "name": "StateProvince", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }
]
},
{ "name": "Rooms", "type": "Collection(Edm.ComplexType)",
"fields": [
{ "name": "Description", "type": "Edm.String", "searchable": true, "analyzer": "en.lucene" },
{ "name": "Description_fr", "type": "Edm.String", "searchable": true, "analyzer": "fr.lucene" },
{ "name": "Type", "type": "Edm.String", "searchable": true },
{ "name": "BaseRate", "type": "Edm.Double", "filterable": true, "facetable": true },
{ "name": "BedOptions", "type": "Edm.String", "searchable": true, "filterable": true, "facetable": false },
{ "name": "SleepsCount", "type": "Edm.Int32", "filterable": true, "facetable": true },
{ "name": "SmokingAllowed", "type": "Edm.Boolean", "filterable": true, "facetable": false},
{ "name": "Tags", "type": "Edm.Collection", "searchable": true }
]
}
]
}
```


Given the previous result set and the above index schema, you have all the required components for a successful indexing operation. The flattened data set meets indexing requirements yet preserves detail information. In the Azure AI Search index, search results fall easily into hotel-based entities, while preserving the context of individual rooms and their attributes.

## Facet behavior on complex type subfields

Fields that have a parent, such as the fields under Address and Rooms, are called *subfields*. Although you can assign a "facetable" attribute to a subfield, the count of the facet is always for the main document.

For complex types like Address, where there's just one "Address/City" or "Address/stateProvince" in the document, the facet behavior works as expected. However, in the case of Rooms, where there are multiple subdocuments for each main document, the facet counts can be misleading.

As noted in [Model complex types](search-howto-complex-data-types): "the document counts returned in the facet results are calculated for the parent document (a hotel), not the subdocuments in a complex collection (rooms). For example, suppose a hotel has 20 rooms of type "suite". Given this facet parameter facet=Rooms/Type, the facet count is one for the hotel, not 20 for the rooms."

## Next steps

Using your own data set, you can use the [Import data wizard](search-import-data-portal) to create and load the index. The wizard detects the embedded JSON collection, such as the one contained in *Rooms*, and infers an index schema that includes a complex type collection.

Try the following quickstart to learn the basic steps of the Import data wizard.
