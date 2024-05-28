# Check the fragmentation for a table

```sql
SELECT
table_name,
round(data_length / 1024 / 1024) AS 'total (MB)',
round(data_free / 1024 / 1024) AS 'unused (MB)',
data_free * 100 / data_length AS 'fragmented (%)'
FROM information_schema.tables
WHERE table_schema = 'my_db'
ORDER BY data_free DESC;
```
