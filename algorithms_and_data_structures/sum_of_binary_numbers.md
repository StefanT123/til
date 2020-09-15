# Sum of binary numbers

Given two binary strings, return their sum (also a binary string).

The input strings are both non-empty and contains only characters 1 or 0.

Example 1:
Input: a = "11", b = "1"
Output: "100"

Example 2:
Input: a = "1010", b = "1011"
Output: "10101"

Constraints:
- Each string consists only of '0' or '1' characters.
- 1 <= a.length, b.length <= 10^4
- Each string is either "0" or doesn't contain any leading zero.

```php
class Solution {

    /**
     * @param String $a
     * @param String $b
     * @return String
     */
    function addBinary($a, $b) {
        $aLen = strlen($a);
        $bLen = strlen($b);
        $max = $aLen > $bLen ? $aLen : $bLen;

        $a = str_pad($a, $max, 0, STR_PAD_LEFT);
        $b = str_pad($b, $max, 0, STR_PAD_LEFT);
        $remainder = 0;
        $res = '';

        for ($i = $max - 1; $i >= 0; $i--) {
            $sum = $a[$i] + $b[$i] + $remainder;

            if ($sum <= 1) {
                $res .= "{$sum}";
                $remainder = 0;
            } else {
                $temp = $sum % 2;
                $res .= "{$temp}";
                $remainder = $sum >> 1;
            }

            if ($i === 0) {
                if ($remainder === 1) {
                    $res .= '1';
                }
            }
        }

        return strrev($res);
    }
}
```
