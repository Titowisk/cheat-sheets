# Referência: (DOCS MICROSOFT, 2010)

## Know the performance and scalability characteristics of queries.
## Write correctly formed queries.

> Do not automatically add a DISTINCT clause to SELECT statements. There is no need to include a DISTINCT clause by default. If you find that you need it because duplicate data is returned, the duplicate data may be the result of an incorrect data model or an incorrect join.

> For example, a join of a table with a composite primary key against a table with a foreign key that is referencing only part of the primary key results in duplicate values. You should investigate queries that return redundant data for these problems.

## Return only the rows and columns needed.

> Queries that call other queries that return too many columns and rows to the calling query are another often-overlooked consideration. This includes queries that are written as views or table-valued functions or views. Although views are useful for many reasons, they may return more columns than you need, or they may return all the rows in the underlying table to the calling query.

## Avoid expensive operators such as NOT LIKE.
## Avoid explicit or implicit functions in WHERE clauses.
## Use locking and isolation level hints to minimize locking.
## Use stored procedures or parameterized queries.
## Minimize cursor use.
## Avoid long actions in triggers.
## Use temporary tables and table variables appropriately.
## Limit query and index hints use.
## Fully qualify database objects.


# Referência: (SQLSHACK, 2018)

## OR in the Join Predicate/WHERE Clause Across Multiple Columns 

É muito custoso devido a enorme quantidade de readings que precisa ser feito

## string searching

Normalmente não eficiente no SQL. Mas existem técnicas que podem ajudar a melhorar a perfomance (ver na fonte)

## Over-Indexing a Table
## Under-Indexing a Table
## No Clustered Index/Primary Key
## High Table Count

Um grande número de tabelas em uma consulta, significa uma grande quantidade de planos de execução para processar e selecionar.
Então, estratégias para diminuir esse número ajuda na perfomance;

>What are some useful ways to optimize a query that is suffering due to too many tables?

Move metadata or lookup tables into a separate query that places this data into a temporary table.
Joins that are used to return a single constant can be moved to a parameter or variable.
Break a large query into smaller queries whose data sets can later be joined together when ready.
For very heavily used queries, consider an indexed view to streamline constant access to important data.
Remove unneeded tables, subqueries, and joins.

## Evaluate performance requirements per transaction
>Sometimes databases advertise their performance characteristics and limitations in terms of write and read throughput and latency. Although this may give a high level overview of the major blockers, when evaluating a new database for performance, a more comprehensive approach is to evaluate critical operations (per query and/or per transaction) separately. 

Examples:

- Write throughput and latency when inserting a new row in to table X (with 50M rows) with given constraints and populating rows in related tables.

- Latency when querying the friends of friends of a user when average number of friends is 500.

- Latency of retrieving the top 100 records for the user timeline when user is subscribed to 500 accounts which has X entries per hour.

# Reference: sqlshack

## Table Indexes and Statistics
The plan will be created based on the query processor tree, resulting from the binding step, and the database tables and indexes statistics, that describes the distribution and uniqueness of the data within the database objects, making sure that the optimization level setting is configured as Full. These statistics help the SQL Server Query Optimizer to compare the number of records returned from scanning all the table rows and the records returned from using different indexes, with the cost of each operation. It is very important to keep the statistics of the database tables and indexes up to date, in order to be able to create the most optimal execution plan.

## Stored Procedures
Reusing execution plans is very beneficial in the case of stored procedures that are executed frequently with different parameters but are still using the same cached execution plan.

## Subtree Cost of the Operator
We usually concentrate on the subtree cost of the operator that represents the execution tree that the SQL Server Engine has looked at so far, from right to left, and top to bottom. In the complex plans, that consists of large number of operators, the full cost of the plan can be derived from the final operation accumulatively.



Fontes:
- https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff647793(v=pandp.10)?redirectedfrom=MSDN#queries
- https://www.sqlshack.com/query-optimization-techniques-in-sql-server-tips-and-tricks/
- https://medium.com/@rakyll/things-i-wished-more-developers-knew-about-databases-2d0178464f78
- https://www.sqlshack.com/how-to-analyze-sql-execution-plan-graphical-components/
