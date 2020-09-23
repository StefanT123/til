# Minimum depth of binary tree

Given a binary tree, find its minimum depth.
The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

`Note:` A leaf is a node with no children.

`Example:`
Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its minimum depth = 2.

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
     * @return Integer
     */
    function minDepth($root) {
        if (! $root) {
            return 0;
        }

        $left = $this->minDepth($root->left);
        $right = $this->minDepth($root->right);

        if (! $left || ! $right) {
            return max($left, $right) + 1;
        }

        return min($left, $right) + 1;
    }
}
```
