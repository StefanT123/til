# Joins

This query means that we `inner join` (in mysql the default join is `inner join`) addresses on stores with the condition that `address_id` in `store` is equal to `address` `id`. Inner join means give me results ONLY if there is a match up
```sql
SELECT *
FROM store
JOIN address
ON store.address_id = address.id;
```

`left join` is the SAME as `left outer join`. What this query does is that if there is no match for the condition that `address_id` in `store` is equal to `address` `id`, I want you to favor left side (store). That will show ALL RESULTS FROM THE STORE TABLE and if there isn't match in the addresses table then for each column in the address table the data will be NULL
```sql
SELECT *
FROM store
LEFT JOIN address
ON store.address_id = address.id;
```

`right join` is the SAME as `right outer join`. What this query does is that if there is no match for the condition that `address_id` in `store` is equal to `address` `id`, I want you to favor right side (address). That will show ALL RESULTS FROM THE ADDRESS TABLE and if there isn't match in the store table then for each column in the store table the data will be NULL
```sql
SELECT *
FROM store
RIGHT JOIN address
ON store.address_id = address.id;
```
