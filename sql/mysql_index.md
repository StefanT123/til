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
