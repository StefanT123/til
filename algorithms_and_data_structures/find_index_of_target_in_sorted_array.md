# Find index of target in sorted array

Given a sorted array and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

`Example 1:`
Input: [1,3,5,6], 5
Output: 2

`Example 2:`
Input: [1,3,5,6], 2
Output: 1

`Example 3:`
Input: [1,3,5,6], 7
Output: 4

`Example 4:`
Input: [1,3,5,6], 0
Output: 0

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer
     */
    function searchInsert($nums, $target) {
        $min = 0;
        $max = count($nums) - 1;

        while ($max >= $min) {
            $guess = ($max + $min) >> 1;

            if ($nums[$guess] === $target) {
                return $guess;
            }

            if ($nums[$guess] < $target) {
                $min = $guess + 1;
            } else {
                $max = $guess - 1;
            }
        }

        return $min;
    }
}
```
