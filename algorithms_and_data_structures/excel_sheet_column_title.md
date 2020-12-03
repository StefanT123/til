# Excel sheet column title

Given a positive integer, return its corresponding column title as appear in an Excel sheet.

For example:

    1 -> A
    2 -> B
    3 -> C
    ...
    26 -> Z
    27 -> AA
    28 -> AB
    ...

Example 1:

    Input: 1
    Output: "A"

Example 2:

    Input: 28
    Output: "AB"

Example 3:

    Input: 701
    Output: "ZY"

```php
class Solution {
    const NUM_OF_LETTERS = 26;
    const LETTER_MAP = ['A','B','C','D','E','F','G','H','I','J','K','L','M','N','O','P','Q','R','S','T','U','V','W','X','Y','Z'];

    /**
     * @param Integer $n
     * @return String
     */
    function convertToTitle($n) {
        $str = '';

        while ($n > 0) {
            $n -= 1;
            $letterIndex = $n % self::NUM_OF_LETTERS;
            $n = ~~($n / self::NUM_OF_LETTERS);
            $str = self::LETTER_MAP[$letterIndex] . $str;
        }

        return $str;
    }
}
```
