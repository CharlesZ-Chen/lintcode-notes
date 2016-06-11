[103. Linked List Cycle II](http://www.lintcode.com/problem/linked-list-cycle-ii)

- [prev: 102. Linked List Cycle](102-linked-list-cycle.md)
- [next: 104. Merge k Sorted Lists](104-merge-k-sorted-lists.md)

---

## My original code
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
     * @return: The node where the cycle begins. 
     *           if there is no cycle, return null
     */
    public ListNode detectCycle(ListNode head) {  
        if (head == null) {
            return null;
        }

        ListNode slow = head;
        ListNode fast = head.next;

        /*=== code could write conciser start ===*/
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) {
                break;
            }
        }

        if (slow != fast) {
            return null;
        }
        /*=== code could write conciser end ===*/

        ListNode k = head;
        slow = slow.next;

        while (k != slow) {
            k = k.next;
            slow = slow.next;
        }

        return k;
    }
}

```

## Little code enhanced
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
     * @return: The node where the cycle begins. 
     *           if there is no cycle, return null
     */
    public ListNode detectCycle(ListNode head) {  
        if (head == null) {
            return null;
        }

        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != slow) {
            if (fast == null || fast.next == null) {
                return null;
            }
            slow = slow.next;
            fast = fast.next.next;
        }

        ListNode k = head;

        while (k != slow.next) {
            k = k.next;
            slow = slow.next;
        }

        return k;
    }
}

```

---

- [prev: 102. Linked List Cycle](102-linked-list-cycle.md)
- [next: 104. Merge k Sorted Lists](104-merge-k-sorted-lists.md)
