[102. Linked List Cycle](http://www.lintcode.com/problem/linked-list-cycle)

- [prev: 101. Remove Duplicates from Sorted Array II](101-remove-duplicates-from-sorted-array-ii.md)
- [next: 103. Linked List Cycle II](103-linked-list-cycle-ii.md)

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
     * @param head: The first node of linked list.
     * @return: True if it has a cycle, or false
     */
    public boolean hasCycle(ListNode head) {
        if (head == null) {
            return false;
        }
        // return hashWay(head);
        return twoPointersWay(head);
    }

    private boolean hashWay(ListNode head) {
        HashSet<ListNode> set = new HashSet();

        while (head != null) {
            if (set.contains(head)) {
                return true;
            } else {
                set.add(head);
                head = head.next;
            }
        }

        return false;
    }

    private boolean twoPointersWay(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                return true;
            }
        }

        return false;
    }
}

```

---

- [prev: 101. Remove Duplicates from Sorted Array II](101-remove-duplicates-from-sorted-array-ii.md)
- [next: 103. Linked List Cycle II](103-linked-list-cycle-ii.md)
