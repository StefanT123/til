# Fulltext indexes

With `FULLTEXT` indexes on the two important fields in the web pages table, it is now easy to do a proper search through the table
```sql
ALTER TABLE webpages ADD FULLTEXT (title);
ALTER TABLE webpages ADD FULLTEXT (content);
```

Allowing visitors to use boolean search techniques with the following query:
```sql
SELECT id FROM webpages WHERE MATCH(title, content) AGAINST ('$searchCriteria' IN BOOLEAN MODE);
```

This time visitors can search for pages and find any pages that have a matching title or even matching content, and they can use +, -, or phrase searching to get more control over the results.
