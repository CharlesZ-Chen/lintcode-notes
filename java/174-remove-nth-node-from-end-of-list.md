[174. Remove Nth Node From End of List](http://www.lintcode.com/problem/remove-nth-node-from-end-of-list)

- [prev: 173. Insertion Sort List](173-insertion-sort-list.md)
- [next: 175. Invert Binary Tree](175-invert-binary-tree.md)

---

Typical application of two pointers.

##Little code readability optimization

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
     * @param n: An integer.
     * @return: The head of linked list.
     */
    ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || n < 0) {
            return null;
        }

        ListNode slow = head;
        ListNode fast = head;

        int i = 0;
        while (i < n && fast != null) {
            fast = fast.next;
            i++;
        }

        if (i != n) {
            return null; //we don't have enough elements in the list
        }

        ListNode prev = null;
        while (fast != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next;
        }

        if (slow == head) {
            return head.next;
        }

        if (slow != null) {
            prev.next = slow.next;
        }

        return head;
    }
}
```

##Original solution
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
     * @param n: An integer.
     * @return: The head of linked list.
     */
    ListNode removeNthFromEnd(ListNode head, int n) {
        if (head == null || n < 0) {
            return null;
        }

        ListNode slow = head;
        ListNode fast = head;

        int i = 0;
        while (i < n) {
            if (fast != null) {
                fast = fast.next;
            } else if ( i != n) {
                return null;
            }
            i++;
        }

        ListNode prev = null;
        while (fast != null) {
            prev = slow;
            slow = slow.next;
            fast = fast.next;
        }

        if (slow == head) {
            return head.next;
        }

        if (slow == null) {
            prev.next = null;
        } else {
            prev.next = slow.next;
        }

        return head;
    }
}

```
---

- [prev: 173. Insertion Sort List](173-insertion-sort-list.md)
- [next: 175. Invert Binary Tree](175-invert-binary-tree.md)
