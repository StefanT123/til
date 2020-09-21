# Convert sorted array to Balanced Search Tree (BST)

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

`Example:`
Given the sorted array: [-10,-3,0,5,9],
One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5

```php
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {

    /**
     * @param Integer[] $nums
     * @return TreeNode
     */
    function sortedArrayToBST($nums) {
        $end = count($nums) - 1;

        return $this->convert($nums, 0, $end);
    }

    protected function convert($arr, $start, $end) {
        /* Base Case */
        if ($start > $end) {
            return null;
        }

        /* Get the middle element and make it root */
        $mid = floor(($start + $end) / 2);
        $node = new TreeNode($arr[$mid]);

        /* Recursively construct the left subtree and make it
         left child of root */
        $node->left = $this->convert($arr, $start, $mid - 1);

        /* Recursively construct the right subtree and make it
         right child of root */
        $node->right = $this->convert($arr, $mid + 1, $end);

        return $node;
    }
}
```
