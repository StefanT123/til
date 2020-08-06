# Difference between two dates in days

```php
function dateDiff($date1, $date2) {
    $SECONDS_IN_YEAR = 31556926;
    $SECONDS_IN_MONTH = 604800;
    $SECONDS_IN_DAY = 86400;

    // find the absoulte difference between the dates in seconds
    $diffInSecs = abs(strtotime($date1) - strtotime($date2));

    // find how many years have passed in days
    $yearsInDays = ($diffInSecs / $SECONDS_IN_YEAR) % 12 * 365;
    // find how many weeks have passed in days
    $weeksInDays = ($diffInSecs / $SECONDS_IN_MONTH) % 52 * 7;
    // find how many days have passed
    $days = ($diffInSecs / $SECONDS_IN_DAY) % 7;

    return $yearsInDays + $weeksInDays + $days;
}


echo dateDiff("2018-01-01", "2019-03-07");
```
