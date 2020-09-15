# Palindrome number

Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

`Example 1:`
Input: 121
Output: true

`Example 2:`
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

`Example 3:`
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

`Follow up:`
Coud you solve it without converting the integer to a string?

```php
class Solution {

    /**
     * @param Integer $x
     * @return Boolean
     */
    function isPalindrome($x) {
        if ($x < 0) {
            return false;
        }

        if ($x < 10) {
            return true;
        }

        $numDigits = strlen($x);
        $reverseInt = 0;
        $num = $x;

        for ($i = 1, $pow = $numDigits - 1; $i <= $numDigits; $i++, $pow--) {
            $digit = $num % 10;
            $num = floor($num / 10);
            $reverseInt += $digit * (10 ** $pow);
        }

        return $x === $reverseInt;
    }
}
```
