# PDO

To connect to a database using `PDO`, you create a new instance of the `PDO` class and give it a data source name (DSN). A DNS is a special string containing connection instructions: what kind of database do we want to connect to, and where is it? When you connect to `MySQL` you need to provide a database name in your DSN, but this isn’t required for `SQLite` because each file holds only one database.
```php
$db = new PDO("mysql:host=localhost;dbname=phpdb", "username", "password");
$result = $db->query("SELECT * FROM coders;");

while ($row = $result->fetch(PDO::FETCH_ASSOC)) {
    print("{$row["name"]} created {$row["languge"]}<br />");
}
```

Using `SQLite`
```php
$db = new PDO("sqlite:coders.sqlite", "username", "password");
$result = $db->query("SELECT * FROM coders;");
$rows = $result->fetchAll(PDO::FETCH_ASSOC);

foreach ($rows as $row) {
    print("{$row["name"]} created {$row["language"]}<br />");
}
```

Line two is where the prepared statement is created, and line three is where it’s executed. Look in the query string and you’ll see :prefix – that’s a placeholder for where some data will go later. Databases are capable of reading this partial SQL, and preparing to execute it as soon as data comes in; hence the name “prepared statements.”

To run the query, the `execute()` method is called on the prepared statement object, and we pass in the values for the placeholders. This is an associative array where the keys match the placeholder names, and the values should be the data to put in there. When you use prepared statements there’s no need to escape any values or worry about quotes around strings – PDO does all that work for us. Plus, because all we’re changing are the values inside the query, you can execute prepared statements significantly faster than regular queries.

**WE SHOULD ALWAYS USE PDO FOR EVERYTHING, and most importantly use `prepare()` and `execute()` to keep your security tight and performance high.**
```php
$prefix = "p%";
$statement = $db->prepare("SELECT * FROM Coders WHERE Language LIKE :prefix;");
$statement->execute([":prefix" => $prefix]);
$rows = $statement->fetchAll(PDO::FETCH_ASSOC);
```
