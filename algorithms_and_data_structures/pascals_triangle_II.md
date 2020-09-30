# Pascal's triangle II

Given an integer `rowIndex`, return the `rowIndex-th` row of the Pascal's triangle.

Notice that the row index starts from `0`.

Could you optimize your algorithm to use only O(k) extra space?

```php
class Solution {

    /**
     * @param Integer $rowIndex
     * @return Integer[]
     */
    function getRow($rowIndex) {
        $triangleArr = [1];

        for ($i = 1; $i <= $rowIndex; $i++) {
            $temp = $triangleArr;
            $triangleArr[0] = 1;

            for ($y = 1; $y < $i; $y++) {
                $triangleArr[$y] += $temp[$y - 1];
            }

            $triangleArr[$i] = 1;
        }

        return $triangleArr;
    }
}
```
