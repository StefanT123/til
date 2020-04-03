# Analyse table for optimal types

We have already looked at various possible data types for varying field information, however they are just very rough guidelines - with MySQL, you can ask it what is the optimal data type for a table, and it will analyse its contents and give you an accurate answer. By "optimal", I mean that the recommended field will be the fastest and/or smallest.

The way to do this is appending PROCEDURE ANALYSE() to your SELECT queries. For example, to have MySQL recommend the best fields to use for our usertable table

By default, PROCEDURE ANALYSE() will analyse character fields and, if they contain very few values, recommend an ENUM data type - this is often not wanted, and you can disable that by using PROCEDURE ANALYSE(1,1), which forces MySQL to not use enum fields when they would contain more than one value or take more than 1 byte.

In the output for that query, there'll be a column "Optimal_fieldtype" - that is the important field to look at, and will contain the best field type for that field based upon existing data. That last bit is important - PROCEDURE ANALYSE() can only analyse what is in your table already, which means if it recommends VARCHAR(9), it does so thinking that you are never going to want to include a ten-character string field.
```sql
SELECT * FROM users PROCEDURE ANALYSE(1,1);
```
