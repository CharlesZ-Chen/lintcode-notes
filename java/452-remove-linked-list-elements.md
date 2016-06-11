[452. Remove Linked List Elements](http://www.lintcode.com/problem/remove-linked-list-elements)

- [prev: 451. Swap Nodes in Pairs](451-swap-nodes-in-pairs.md)
- [next: 453. Flatten Binary Tree to Linked List](453-flatten-binary-tree-to-linked-list.md)

---

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param head a ListNode
     * @param val an integer
     * @return a ListNode
     */
    public ListNode removeElements(ListNode head, int val) {
        if (head == null) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode preDel = dummy;

        while (head != null) {
            if (head.val == val) {
                preDel.next = preDel.next.next;
            } else {
                preDel = preDel.next;
            }
            head = head.next;
        }

        return dummy.next;
    }
}
```

---

- [prev: 451. Swap Nodes in Pairs](451-swap-nodes-in-pairs.md)
- [next: 453. Flatten Binary Tree to Linked List](453-flatten-binary-tree-to-linked-list.md)
