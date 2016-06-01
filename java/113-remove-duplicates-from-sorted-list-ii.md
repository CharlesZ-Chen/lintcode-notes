[113. Remove Duplicates from Sorted List II](http://www.lintcode.com/problem/remove-duplicates-from-sorted-list-ii)

- [prev: 112. Remove Duplicates from Sorted List](112-remove-duplicates-from-sorted-list.md)
- [next: 114. Unique Paths](114-unique-paths.md)

---

#One time pass! Vola!

Typical application of `dummy node` plus `two pointers`.

```java
/**
 * Definition for ListNode
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) {
 *         val = x;
 *         next = null;
 *     }
 * }
 */
public class Solution {
    /**
     * @param ListNode head is the head of the linked list
     * @return: ListNode head of the linked list
     */
    public static ListNode deleteDuplicates(ListNode head) {
        if (head == null) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode preDel = dummy;
        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != null) {
            slow = preDel.next;
            fast = slow == null ? null : slow.next;

            if (fast == null) {
                break;
            }

            if (slow.val != fast.val) {
                preDel = preDel.next;
                continue;
            }

            while (fast != null && slow.val == fast.val) {
                fast = fast.next;
            }

            preDel.next = fast;
        }

        return dummy.next;
    }
}

```

---

- [prev: 112. Remove Duplicates from Sorted List](112-remove-duplicates-from-sorted-list.md)
- [next: 114. Unique Paths](114-unique-paths.md)
