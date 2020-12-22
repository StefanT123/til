# MySql index

### What does indexing in MySql does?

When we index some column in MySQL, behind the scenes MySql will order the table by that column and it will store the table (it doesn't actually store the table multiple times, it just stores pointers into the table). So whenever we want to access some data that's in that table, it will do a search with `binary search algorithm` to find that data.

ADD INDEX('name') - it stores the whole table ordered by name
| name   | date       |
|--------|------------|
| Anna   | 2020-07-25 |
| Anna   | 2017-01-26 |
| Antony | 2018-01-10 |
| Antony | 2017-06-12 |
| Juliet | 2017-07-18 |
| Leone  | 2019-03-13 |
| Leone  | 2019-12-01 |

ADD INDEX('date') - it stores the whole table ordered by date
| name   | date       |
|--------|------------|
| Anna   | 2017-01-26 |
| Antony | 2017-06-12 |
| Juliet | 2017-07-18 |
| Antony | 2018-01-10 |
| Leone  | 2019-03-13 |
| Leone  | 2019-12-01 |
| Anna   | 2020-07-25 |

ADD INDEX('name', date') - it stores the whole table ordered by name, and for those that have the same name, it orders them by date
| name   | date       |
|--------|------------|
| Anna   | 2017-01-26 |
| Anna   | 2020-07-25 |
| Antony | 2017-06-12 |
| Antony | 2018-01-10 |
| Juliet | 2017-07-18 |
| Leone  | 2019-03-13 |
| Leone  | 2019-12-01 |


#### Types of indexes
- PRIMARY INDEX - Unique and not NULL (PRIMARY KEY)
- UNIQUE INDEX - Unique, mutliple NULLs are allowed, search stops after finding it (only one unique index or null)
- INDEX - Just an ordinary index, search stops after finding it (Normal index)
- FULLTEXT INDEX - Text-searching index (MATCH vs LIKE)
- COMPOSITE INDEX
  - Contains more than one column
  - COVERING INDEX
    - Contains all fields in query

#### What to index?
- FOREIGN KEY (for JOINs)
- WHERE (ex. if we have users table, we have to find all the usages of that table, EVERYWHERE to understand which columns are used in where statement)
- ORDER BY
- SELECT columns*

##### FOR COMPOISTE INDEX THE FIRST INDEX SHOULD ALWAYS BE THE COLUMN THAT HAS LESS RESULTS IN THE TABLE
##### COVERING INDEX is the best type of index, but it's hard to make it if you have many fields with different queries

#### When indexes do and don't work
| Numbers                           | Strings                              |
|-----------------------------------|--------------------------------------|
| column = 5 (work)                 | column1 = 'asd' (work)               |
| column BETWEEN 1 AND 5 (work)     | column1 > column2 (work)             |
| column > 5 (not very good)        | column LIKE ('ABC%') (work)          |
| column in (1,2,3) (doesn't work)  | column LIKE ('%ABC$') (doesn't work) |

#### Index JOIN types
- system - the table has only zero or one row
- const - the table has only one matching row which is indexed. This is the fastes type of join because the table only has to be read once and the columns value can be treated as a constant when joining other tables
- eq_ref - all parts of an index are used by the join and the index is PRIMARY KEY or UNIQUE NOT NULL. This is the nex best possible join type
- ref - all of the matching rows of an indexed column are read for each combination of rows fromthe previous table. This type of join appears for indexed columns compared using = or <=> operators
- fulltext - the join uses tables FULLTEXT index
- ref_or_null - this is the same as ref but also contains rows with a null value for the column
- index_merge - the join uses a list of indexes to produce the result set. The key column of EXPLAINs output will contain the keys used
- unique_subquery - an IN subquery returns only one result from the table and makes use of the primary key
- index_subquery - the same as unique_subquery but returns more than one result row
- range - an index used to find matching rows in a specific range, typically when the key column is compared to a constant using operators like BETWEEN, IN, >, >=, etc.
- index - the entire index tree is scanned to find matching rows
- all - the entire table is scanned to find matching rows for the join. This is the worst join type and usually indicates the lack of appropriate indexes on the table
