---
source_url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SQLtoNoSQL.RemoveTable.html
fetched_at: 2026-01-25T12:26:14.362238
---

# Differences between a relational (SQL) database
                and DynamoDB when removing a table

# Differences between a relational (SQL) database and DynamoDB when removing a table

In SQL, you use the `DROP TABLE`

statement to remove a table. In Amazon DynamoDB,
you use the `DeleteTable`

operation.

## Removing a table with SQL

When you no longer need a table and want to discard it permanently, you would use
the `DROP TABLE`

statement in SQL.

`DROP TABLE Music;`


After a table is dropped, it cannot be recovered. (Some relational databases do
allow you to undo a `DROP TABLE`

operation, but this is vendor-specific
functionality and it is not widely implemented.)

## Removing a table in DynamoDB

In DynamoDB, `DeleteTable`

is a similar operation. In the following
example, the table is permanently deleted.

`{ TableName: "Music" }`