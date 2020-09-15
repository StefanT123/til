# Plus one

Given a non-empty array of digits representing a non-negative integer, increment one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contains a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.



`Example 1:`
Input: digits = [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.

`Example 2:`
Input: digits = [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.

`Example 3:`
Input: digits = [0]
Output: [1]

`Constraints:`
1 <= digits.length <= 100
0 <= digits[i] <= 9

```php
class Solution {

    /**
     * @param Integer[] $digits
     * @return Integer[]
     */
    function plusOne($digits) {
        $digitsLen = count($digits);

        for ($i = $digitsLen - 1; $i >= 0; $i--) {
            if ($digits[$i] < 9) {
                $digits[$i]++;
                break;
            }

            if ($digits[$i] === 9) {
                $digits[$i] = 0;

                if (! $digits[$i - 1]) {
                    array_unshift($digits, 1);
                }
            }
        }

        return $digits;
    }
}
```
