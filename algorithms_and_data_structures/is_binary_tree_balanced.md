# Is binary tree balanced

Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as:
`a binary tree in which the left and right subtrees of every node differ in height by no more than 1.`

Example 1:
Given the following tree [3,9,20,null,null,15,7]:

    3
   / \
  9  20
    /  \
   15   7
Return true.

Example 2:
Given the following tree [1,2,2,3,3,null,null,4,4]:

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
Return false.

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
    protected $isBalanced = true;

    /**
     * @param TreeNode $root
     * @return Boolean
     */
    function isBalanced($root) {
        $this->check($root);

        return $this->isBalanced;
    }

    protected function check($node) {
        if (! $this->isBalanced) {
            return false;
        }

        if (! $node) {
            return false;
        }

        $left = $this->check($node->left);
        $right = $this->check($node->right);

        if (abs($left - $right) > 1) {
            $this->isBalanced = false;
        }

        return max($left, $right) + 1;
    }
}
```
