# Move table from one database to another in the same cluster

```sql
"CREATE TABLE IF NOT EXISTS toDatabase.table LIKE fromDatabase.table"

"RENAME TABLE fromDatabase.table TO fromDatabase.table_new, toDatabase.table TO fromDatabase.table, fromDatabase.table_new TO toDatabase.table"
```
