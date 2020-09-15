# Merge sorted array

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:
- The number of elements initialized in nums1 and nums2 are m and n respectively.
- You may assume that nums1 has enough space (size that is equal to m + n) to hold additional elements from nums2.

Example:
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]


Constraints:
- -10^9 <= nums1[i], nums2[i] <= 10^9
- nums1.length == m + n
- nums2.length == n

```php
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer $m
     * @param Integer[] $nums2
     * @param Integer $n
     * @return NULL
     */
    function merge(&$nums1, $m, $nums2, $n) {
        $tail1 = $m - 1;
        $tail2 = $n - 1;
        $finished = $m + $n - 1;

        while ($tail2 >= 0) {
            $nums1[$finished--] = $nums1[$tail1] > $nums2[$tail2] ? $nums1[$tail1--] : $nums2[$tail2--];
        }
    }
}
```
