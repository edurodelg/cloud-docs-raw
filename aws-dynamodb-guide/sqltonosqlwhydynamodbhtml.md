---
source_url: https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/SQLtoNoSQL.WhyDynamoDB.html
fetched_at: 2026-01-28T07:15:46.671772
---

# Choosing between relational (SQL) and
                NoSQL

# Choosing between relational (SQL) and NoSQL

Today's applications have more demanding requirements than ever before. For example, an online game might start out with just a few users and a very small amount of data. However, if the game becomes successful, it can easily outstrip the resources of the underlying database management system. It is common for web-based applications to have hundreds, thousands, or millions of concurrent users, with terabytes or more of new data generated per day. Databases for such applications must handle tens (or hundreds) of thousands of reads and writes per second.

Amazon DynamoDB is well-suited for these kinds of workloads. As a developer, you can start small and gradually increase your utilization as your application becomes more popular. DynamoDB scales seamlessly to handle very large amounts of data and very large numbers of users.

For more information on traditional relational database modeling and how to adapt it
for DynamoDB, see [Best practices for modeling relational data in
DynamoDB](./bp-relational-modeling.html).

The following table shows some high-level differences between a relational database management system (RDBMS) and DynamoDB.

| Characteristic | Relational database management system (RDBMS) | Amazon DynamoDB |
|---|---|---|
Optimal Workloads |
Ad hoc queries; data warehousing; OLAP (online analytical processing). | Web-scale applications, including social networks, gaming, media sharing, and Internet of Things (IoT). |
Data Model |
The relational model requires a well-defined schema, where data is normalized into tables, rows, and columns. In addition, all of the relationships are defined among tables, columns, indexes, and other database elements. | DynamoDB is schemaless. Every table must have a primary key to uniquely identify each data item, but there are no similar constraints on other non-key attributes. DynamoDB can manage structured or semistructured data, including JSON documents. |
Data Access |
SQL is the standard for storing and retrieving data. Relational databases offer a rich set of tools for simplifying the development of database-driven applications, but all of these tools use SQL. | You can use the AWS Management Console, the AWS CLI, or NoSQL WorkBench to work with
DynamoDB and perform ad hoc tasks.
|

**Performance****Scaling**