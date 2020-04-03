# WHERE clauses with AND and OR

MySQL allows you to perform more complicated queries by using AND and OR in your WHERE clause to tie conditions together. You can also use brackets to form groups of equations through two main processes - using AND/OR (plus brackets) to make your queries more specific, and using the JOIN keyword to merge tables together
```sql
SELECT * FROM users WHERE first_name = 'John' AND last_name = 'Smith';
SELECT * FROM users WHERE first_name = 'John' AND (last_name = 'Smith' OR last_name = 'Jones');
SELECT * FROM users WHERE (first_name = 'John' OR first_name = 'Jennifer') AND (last_name = 'Smith' OR last_name = 'Jones');
```
