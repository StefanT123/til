# Setting priorities

In order to make changes to your data happen as you would expect, MySQL has a fairly basic priority queuing system in place - by default, writing data has a higher priority than reading data, which means if you have a number of SELECT queries piled up and one UPDATE query comes in, the UPDATE query gets push to the front of the queue and executed first. This makes sure that SELECT queries always read from the most up to date information available, which is generally the desired behaviour.

There are two ways you can temporarily alter MySQL's queuing - you can push a SELECT query up to a higher level as a write query, or you can push a write query down to a lower level than a SELECT query. Both are done on a query-by-query basis - you specify in the query that you want it to have special priority.

To make a SELECT query a higher priority as a write query, which means that if you have a SELECT query waiting to be executed and a write query comes into the queue, it will not push in front of the SELECT query, you use the HIGH_PRIORITY modifier

High priority SELECT queries will always out-rank table writes, which mean that if you have five table writes in a queue, it is possible that they may never get done - if you keep sending in SELECT queries marked as high priority, they will keep pushing ahead of the writes.

To push a write query down to a lower priority than a SELECT, use the LOW_PRIORITY keyword. In this situation, a write is considered to be less important than SELECT queries, which means that it will wait for all reading to complete before writing, even if new reads come in after it. As such, it is possible for low priority writes to never get done - as long as you keep putting more reads in, they will continue to out-rank the low priority writes. Here is a low priority write in action.
```sql
SELECT HIGH_PRIORITY first_name FROM users;
INSERT LOW_PRIORITY INTO users VALUES (24, "Joe", "Blow", 42);
```
