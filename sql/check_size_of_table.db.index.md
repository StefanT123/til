# Check size of table, DB, index

### Check size of table in DB
```sql
SELECT table_schema AS "Database",
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS "Size (MB)"
FROM information_schema.tables
WHERE table_schema = 'my_db'
GROUP BY table_schema;
```

### Check size of each DB on the server
```sql
SELECT table_schema AS "Database",
    ROUND(SUM(data_length + index_length) / 1024 / 1024, 2) AS "Size (MB)"
FROM information_schema.tables
GROUP BY table_schema;
```

### Check size of specific table in DB
```sql
SELECT TABLE_NAME AS "Table",
    ROUND(((data_length + index_length) / 1024 / 1024), 2) AS "Size (MB)"
FROM information_schema.tables
WHERE table_schema = 'my_db' AND TABLE_NAME = 'my_table';
```

### Check all table sizes from all DBs
```sql
SELECT table_schema AS "Database",
    TABLE_NAME AS "Table",
    ROUND(((data_length + index_length) / 1024 / 1024), 2) AS "Size (MB)"
FROM information_schema.tables
ORDER BY data_length + index_length DESC;
```

### Check size of indexes for a specific table
```sql
SELECT TABLE_NAME AS "Table",
    ROUND((index_length / 1024 / 1024), 2) AS "Index Size (MB)"
FROM information_schema.tables
WHERE table_schema = 'your_database_name' AND TABLE_NAME = 'your_table_name';
```