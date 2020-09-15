# Reverse integer

Given a 32-bit signed integer, reverse digits of an integer.

`Example 1:`
Input: 123
Output: 321

`Example 2:`
Input: -123
Output: -321

`Example 3:`
Input: 120
Output: 21

`Note:`
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: `[−2^31,  2^31 − 1]`. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

```php
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function reverse($x) {
        if ($x < 0) {
            $x *= -1;
            $switchSign = true;
        }

        $numLength = strlen($x);
        $reversedInt = 0;

        for ($i = 1, $pow = $numLength - 1; $i <= $numLength; $i++, $pow--) {
            $digit = $x % 10;
            $x = floor($x / 10);
            $reversedInt += $digit * (10 ** $pow);
        }

        $reversedInt = $switchSign ? $reversedInt *= -1 : $reversedInt;

        if ($reversedInt < -2147483648 || $reversedInt >  2147483647) {
            return 0;
        }

        return $reversedInt;
    }
}
```
