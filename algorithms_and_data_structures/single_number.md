# Single number

Given a non-empty array of integers nums, every element appears twice except for one. Find that single one.

Follow up: Could you implement a solution with a linear runtime complexity and without using extra memory?

`Example 1:`
Input: nums = [2,2,1]
Output: 1

`Example 2:`
Input: nums = [4,1,2,1,2]
Output: 4

`Example 3:`
Input: nums = [1]
Output: 1

`Constraints:`
1 <= nums.length <= 3 * 104
-3 * 104 <= nums[i] <= 3 * 104
Each element in the array appears twice except for one element which appears only once.

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function singleNumber($nums) {
        $numsLen = count($nums);
        $x = 0;

        for ($i = 0; $i < $numsLen; $i++) {
            $x ^= $nums[$i];
        }

        return $x;
    }
}
```

`Concept:`
- If we take XOR of zero and some bit, it will return that bit
  - a ⊕ 0 = a

- If we take XOR of two same bits, it will return 0
  - a ⊕ a = 0

- a ⊕ b ⊕ a = (a ⊕ a) ⊕ b = 0 ⊕ b = b

So we can XOR all bits together to find the unique number.
