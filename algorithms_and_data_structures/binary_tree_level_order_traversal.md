# Binary tree level order traversal

Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]

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
    protected $finalData = [];

    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrderBottom($root) {
        $this->getNode($root, 0);

        return array_reverse($this->finalData);
    }

    function getNode($node, $level) {
        if ($node !== null) {
            $this->finalData[$level][] = $node->val;
        }

        if ($node->left) {
            $this->getNode($node->left, $level + 1);
        }

        if ($node->right) {
            $this->getNode($node->right, $level + 1);
        }
    }
}
```
