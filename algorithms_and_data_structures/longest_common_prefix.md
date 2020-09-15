# Longest common prefix

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string `""`.

`Example 1:`
Input: ["flower","flow","flight"]
Output: "fl"

`Example 2:`
Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.

`Note:`
All given inputs are in lowercase letters `a-z`.

```php
class Solution {

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs) {
        $numOfStrings = count($strs);
        $prefix = '';
        $letters = [];

        if (! $numOfStrings) {
            return $prefix;
        }

        if ($numOfStrings < 2) {
            return $strs[0];
        }

        for ($i = 0, $y = 0;;) {
            if (! isset($letters[$y])) {
                $letters[$y] = 1;
            }

            if ($strs[$i][$y] !== '' && $strs[$i][$y] === $strs[$i + 1][$y]) {
                $letters[$y]++;

                if ($letters[$y] === $numOfStrings) {
                    $prefix .= $strs[$i][$y];
                    $i = 0;
                    $y++;
                    continue;
                }

                $i++;
                continue;
            }

            break;
        }

        return $prefix;
    }
}
```
