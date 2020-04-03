# Pattern matching (searching)

```sql
LIKE # allows simple pattern matching to be performed on each row
    SELECT * FROM users WHERE first_name LIKE 'Paul%' # the % sign means "any number of characters" (including no characters)
```

```sql
ALTER TABLE users ADD FULLTEXT(first_name); # Once we have a FULLTEXT index on our table, it opens up a whole new world of pattern matching
    CREATE TABLE opinions (Opinion CHAR(100));
    INSERT INTO opinions VALUES ('MySQL is a very fast database');
    INSERT INTO opinions VALUES ('Green is everyone\'s favourite colour');
    INSERT INTO opinions VALUES ('Databases are helpful for storing data');
    INSERT INTO opinions VALUES ('PHP is a very nice language');
    INSERT INTO opinions VALUES ('Spain is a nice country to visit');
    INSERT INTO opinions VALUES ('Perl isn\'t as nice a language as PHP');
    INSERT INTO opinions VALUES ('This is a blank row to avoid the 50% rule');
    ALTER TABLE opinions ADD FULLTEXT (opinion);

    SELECT * FROM opinions WHERE MATCH(opinion) AGAINST ('nice'); # it will find every opinion that contains the word 'nice'

    SELECT * FROM opinions WHERE MATCH(opinion) AGAINST ('nice language'); # matches nice OR language

    SELECT * FROM opinions WHERE MATCH(opinion) AGAINST ('nice -language' IN BOOLEAN MODE); # allow you to proceed words with a + or a - to force it to either be present (+) or not present (-)

    SELECT * FROM opinions WHERE Match(opinion) AGAINST ('"nice language"' IN BOOLEAN MODE) #  putting double quotes around groups of words allow phrase searching ( That is, to match precisely "nice language" )
```
