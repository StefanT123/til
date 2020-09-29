# Pascal's triangle

Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.

`Example:`
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]

```php
class Solution {
    /**
     * @param Integer $numRows
     * @return Integer[][]
     */
    function generate($numRows) {
        $triangleArr = [];

        for ($i = 0; $i < $numRows; $i++) {
            if ($i === 0) {
                $triangleArr[0] = [1];
                continue;
            }

            if ($i === 1) {
                $triangleArr[1] = [1,1];
                continue;
            }

            $triangleArr[$i][0] = 1;

            for ($y = 1; $y < $i; $y++) {
                $numVal = $triangleArr[$i - 1][$y] + $triangleArr[$i - 1][$y - 1];
                $triangleArr[$i][$y] = $numVal;
            }

            $triangleArr[$i][$i] = 1;
        }

        return $triangleArr;
    }
}
```
