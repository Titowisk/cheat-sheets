
- Know the performance and scalability characteristics of queries.
- Write correctly formed queries.

> Do not automatically add a DISTINCT clause to SELECT statements. There is no need to include a DISTINCT clause by default. If you find that you need it because duplicate data is returned, the duplicate data may be the result of an incorrect data model or an incorrect join.

> For example, a join of a table with a composite primary key against a table with a foreign key that is referencing only part of the primary key results in duplicate values. You should investigate queries that return redundant data for these problems.

- Return only the rows and columns needed.
- Avoid expensive operators such as NOT LIKE.
- Avoid explicit or implicit functions in WHERE clauses.
- Use locking and isolation level hints to minimize locking.
- Use stored procedures or parameterized queries.
- Minimize cursor use.
- Avoid long actions in triggers.
- Use temporary tables and table variables appropriately.
- Limit query and index hints use.
- Fully qualify database objects.



Fontes:
https://docs.microsoft.com/en-us/previous-versions/msp-n-p/ff647793(v=pandp.10)?redirectedfrom=MSDN#queries
