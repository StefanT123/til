# Path sum in binary tree

Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.

`Note:` A leaf is a node with no children.

`Example:`
Given the below binary tree and `sum = 22`,

      5
     / \
    4   8
   /   / \
  11  13  4
 /  \      \
7    2      1
return true, as there exist a root-to-leaf path `5->4->11->2` which sum is 22.

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
     * @param Integer $sum
     * @return Boolean
     */
    function hasPathSum($root, $sum) {
        if (! $root) {
            return false;
        }

        if ($root->val === $sum && ! $root->left && ! $root->right) {
            return true;
        }

        return $this->hasPathSum($root->left, $sum - $root->val) ||
            $this->hasPathSum($root->right, $sum - $root->val);
    }
}
```
