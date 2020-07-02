# SQL functions

```sql
AUTO_INCREMENT # it instructs MySQL to insert a unique ID number for you
PRIMARY KEY # instructs MySQL to ruthlessly enforce ID as a unique number
GROUP BY # it is used in collaboration with the SELECT statement to arrange identical data into groups
HAVING # it enables you to specify conditions that filter which group results appear in the results, the WHERE clause places conditions on the selected columns, whereas the HAVING clause places conditions on groups created by the GROUP BY clause
ORDER BY # makes it easy to order your data
RAND() # returns your rows in a random order
    ORDER BY RAND() LIMIT 1 # to pick out one random row from your database
BETWEEN(16,21) # return all records between 16 and 21
SELECT * FROM people WHERE Age IN (19, 20, 21); # allows you to specify the exact range of possibilities that will be matched against

MIN() # return the minimum values of a field you specify
MAX() # return the maximum values of a field you specify
    SELECT MAX(age) FROM users; # finds the oldest person
    #### If the field chosen is a character field, MIN() and MAX() work alphabetically, so MIN() would return "Alex" before "Becky"

COUNT() # returns the number of rows which match your query
    SELECT COUNT(*) FROM users WHERE age > 22; # returns the number of people in your table who are aged 23 or above

SUM() # adds up all the values in the attributes you select
    SELECT SUM(age) FROM users # return the ages of all the people in your table, added up

AVG() # adds up all the values in the attributes you select and divides that result by the number of values, giving the mean average
    SELECT SUM(avg) FROM users # returns the average age of all members

UNIX_TIMESTAMP() # takes a MySQL time as a parameter, and returns the corresponding Unix timestamp
NOW() # returns the current MySQL time
    SELECT * FROM users WHERE last_login_time > UNIX_TIMESTAMP(NOW()) - 86400; # return all users who have logged in in the last 24 hours ( 86400 is the number of seconds in a day )

CONCAT() # takes any number of parameters, and it returns them combined
    SELECT CONCAT(first_name, ' ', last_name) FROM users; # combines first name and last name with a space in the middle
```
