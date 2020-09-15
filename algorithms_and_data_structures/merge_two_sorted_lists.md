# Merge two sorted lists

Merge two sorted linked lists and return it as a new sorted list. The new list should be made by splicing together the nodes of the first two lists.

Example:
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4

```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function mergeTwoLists($l1, $l2) {
        if (! $l1) {
            return $l2;
        }

        if (! $l2) {
            return $l1;
        }

        if ($l1->val <= $l2->val) {
            $l1->next = $this->mergeTwoLists($l1->next, $l2);

            return $l1;
        } else {
            $l2->next = $this->mergeTwoLists($l1, $l2->next);

            return $l2;
        }
    }
}
```
