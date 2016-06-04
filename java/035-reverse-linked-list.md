[035. Reverse Linked List](http://www.lintcode.com/problem/reverse-linked-list)

- [prev: 034. N-Queens II](034-n-queens-ii.md)
- [next: 036. Reverse Linked List II](036-reverse-linked-list-ii.md)

---

```java
/**
 * Definition for ListNode.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int val) {
 *         this.val = val;
 *         this.next = null;
 *     }
 * }
 */ 
public class Solution {
    /**
     * @param head: The head of linked list.
     * @return: The new head of reversed linked list.
     */
    public ListNode reverse(ListNode head) {
        if (head == null) {
            return null;
        }

        ListNode prev = null;
        ListNode curt = head;

        while (curt != null) {
            ListNode temp = curt.next;
            curt.next = prev;
            prev = curt;
            curt = temp;
        }

        return prev;
    }
}
```

---

- [prev: 034. N-Queens II](034-n-queens-ii.md)
- [next: 036. Reverse Linked List II](036-reverse-linked-list-ii.md)
