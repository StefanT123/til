# Is the tree symmetric

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3


But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3

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
     * @param TreeNode $root
     * @return Boolean
     */
    function isSymmetric($root) {
        $arr = [];
        $arr[] = $root;
        $arr[] = $root;

        while (! empty($arr)) {
            $node1 = array_shift($arr);
            $node2 = array_shift($arr);

            if ($node1 === null && $node2 === null) {
                continue;
            }

            if ($node1 === null || $node2 === null) {
                return false;
            }

            if ($node1->val !== $node2->val) {
                return false;
            }

            $arr[] = $node1->left;
            $arr[] = $node2->right;
            $arr[] = $node1->right;
            $arr[] = $node2->left;
        }

        return true;
    }
}
```
