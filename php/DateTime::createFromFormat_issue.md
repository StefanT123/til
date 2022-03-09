# DateTime::createFromFormat('Y-m-d', '0000-00-00') issue

By using `\DateTime::createFromFormat('Y-m-d', $date)` and when `$date` value is "0000-00-00" we're getting:
```php
object(DateTime)#181 (3) {
  ["date"]=>
  string(27) "-0001-11-30 17:30:35.000000"
  ["timezone_type"]=>
  int(3)
  ["timezone"]=>
  string(3) "UTC"
}
```

The correct values for day are 1-31, for month from 1-12, so php tries it's best to get the correct values. So for month it's 12-1 = 11, for day 31-1=30, same for year, that's why we get that result.
