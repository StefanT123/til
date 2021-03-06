# Two Sum (indicies of two numbers that add up together)

Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.

`Example 1:`
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].

`Example 2:`
Input: nums = [3,2,4], target = 6
Output: [1,2]

`Example 3:`
Input: nums = [3,3], target = 6
Output: [0,1]

`Constraints:`
- 2 <= nums.length <= 105
- 109 <= nums[i] <= 109
- 109 <= target <= 109
- Only one valid answer exists.

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        $numsLength = count($nums);
        $resultList = [];

        for ($i = 0; $i < $numsLength; $i++) {
            $res = $target - $nums[$i];

            if (isset($resultList[$res])) {
                return [$resultList[$res], $i];
            }

            $resultList[$nums[$i]] = $i;
        }
    }
}
```

Solution if the array is sorted in ascending order with two pointers:
```php
class Solution {

    /**
     * @param Integer[] $numbers
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($numbers, $target) {
        $left = 0;
        $right = count($numbers) - 1;

        while ($left < $right) {
            $sum = $numbers[$left] + $numbers[$right];

            if ($sum === $target) {
                return [$left + 1, $right + 1];
            }

            if ($sum > $target) {
                $right -= 1;
            } else {
                $left += 1;
            }
        }
    }
}
```
