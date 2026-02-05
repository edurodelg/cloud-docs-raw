---
source_url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SQLtoNoSQL.ReadData.Scan.html
fetched_at: 2026-02-05T08:28:05.037350
---

# Differences in scanning a table

In SQL, a `SELECT`

statement without a `WHERE`

clause will
return every row in a table. In Amazon DynamoDB, the `Scan`

operation does the
same thing. In both cases, you can retrieve all of the items or just some of
them.

Whether you are using a SQL or a NoSQL database, scans should be used sparingly
because they can consume large amounts of system resources. Sometimes a scan is
appropriate (such as scanning a small table) or unavoidable (such as performing a
bulk export of data). However, as a general rule, you should design your
applications to avoid performing scans. For more information, see [Querying tables in DynamoDB](./Query.html).

###### Note

Doing a bulk export also creates at least 1 file per partition. All of the items in each file are from that particular partition's hashed keyspace.

## Scanning a table with SQL

When using SQL you can scan a table and retrieve all of its data by using a
`SELECT`

statement without specifying a `WHERE`

clause. You can request one or more columns in the result. Or you can request
all of them if you use the wildcard character (*).

The following are examples of using a `SELECT`

statement.

`/* Return all of the data in the table */ SELECT * FROM Music;`


`/* Return all of the values for Artist and Title */ SELECT Artist, Title FROM Music;`


## Scanning a table in DynamoDB

In Amazon DynamoDB, you can use either the DynamoDB API or [PartiQL](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/ql-reference.html) (a SQL-compatible query
language) to perform a scan on a table.