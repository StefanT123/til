# Using aliases

We alias `members` and `golf_centers` as `m` and `c` respectively, so when we are referencing columns from those two tables, all we have to do is to prefix the column name with the alias of that table followd by a dot (.).
```sql
SELECT m.id, m.first_name, m.last_name, c.centre_num FROM members m, golf_centres c WHERE m.centre_num = c.id;
```
