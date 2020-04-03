# Selecting data

```sql
SELECT id, last_name FROM users; # selecting data
SELECT * FROM users WHERE age > 30; # "WHERE" allows you to force MySQL to return only rows that match certain criteria
SELECT * FROM users LIMIT 1; #  return a certain number of results
SELECT * FROM users LIMIT 20, 10; # return the first n rows after the first m that match (skip first 20 rows and return the next 10)
SELECT DISTINCT last_name FROM users; # returns all last_names with different values
SELECT CONCAT(first_name, ' ', last_name) AS full_name FROM users; # "CONCAT" is adding first_name and last_name, "AS" lets you change the field names (temporarily) to something more useful to you we will find our array has the "full_name" element set, which is much easier to read and handle.
```
