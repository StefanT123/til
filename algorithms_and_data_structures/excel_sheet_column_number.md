# Excel sheet column number

Given a column title as appear in an Excel sheet, return its corresponding column number.

For example:

    A -> 1
    B -> 2
    C -> 3
    ...
    Z -> 26
    AA -> 27
    AB -> 28
    ...

Example 1:

    Input: "A"
    Output: 1

Example 2:

    Input: "AB"
    Output: 28

Example 3:

    Input: "ZY"
    Output: 701

```php
class Solution {
    const NUM_OF_LETTERS = 26;
    const LETTER_MAP = [
        'A' => 1,
        'B' => 2,
        'C' => 3,
        'D' => 4,
        'E' => 5,
        'F' => 6,
        'G' => 7,
        'H' => 8,
        'I' => 9,
        'J' => 10,
        'K' => 11,
        'L' => 12,
        'M' => 13,
        'N' => 14,
        'O' => 15,
        'P' => 16,
        'Q' => 17,
        'R' => 18,
        'S' => 19,
        'T' => 20,
        'U' => 21,
        'V' => 22,
        'W' => 23,
        'X' => 24,
        'Y' => 25,
        'Z' => 26,
    ];

    /**
     * @param String $s
     * @return Integer
     */
    function titleToNumber($s) {
        if (self::LETTER_MAP[$s]) {
            return self::LETTER_MAP[$s];
        }

        $res = 0;
        $exponent = strlen($s) - 1;
        $arr = str_split($s);

        foreach ($arr as $letter) {
            $res += self::NUM_OF_LETTERS ** $exponent * self::LETTER_MAP[$letter];
            $exponent--;
        }

        return $res;
    }
}
```
