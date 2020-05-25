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



Fontes:
https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff647793(v=pandp.10)?redirectedfrom=MSDN#queries
https://www.sqlshack.com/query-optimization-techniques-in-sql-server-tips-and-tricks/
