[036. Reverse Linked List II](http://www.lintcode.com/problem/reverse-linked-list-ii)

- [prev: 035. Reverse Linked List](035-reverse-linked-list.md)
- [next: 038. Search a 2D Matrix II](038-search-a-2d-matrix-ii.md)

---
## My Solution

This problem isn't a hard one. As long as be clear with the reverse process, this one would be solved.

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
     * @oaram m and n
     * @return: The head of the reversed ListNode
     */
    public ListNode reverseBetween(ListNode head, int m , int n) {
        if (head == null || m < 1 || n < m) {
            return null;
        }

        ListNode dummy = new ListNode(0);
        dummy.next = head;

        ListNode begin, end;

        begin = dummy;
        end = dummy;
        ListNode preBegin = dummy;

        for (int i = 0; i < m; i++) {
            preBegin = begin;
            begin = begin.next;
            end = end.next;
            if (begin == null) {
                return null; // elements in list less than m, invalid input
            }
        }

        for (int i = 0; i < n - m; i++) {
            end = end.next;
            if (end == null) {
                return null; // elements in list less than n, invalid input
            }
        }

        // length is n - m + 1, move m.next need n - m times

        preBegin.next = end;

        ListNode rever = begin.next;
        ListNode pre = begin;
        begin.next = end.next;
        for (int i = 0; i < n - m; i++) {
            ListNode nextRever = rever.next;
            rever.next = pre;
            pre = rever;
            rever = nextRever;
        }

        return dummy.next;
    }
}
```

---

- [prev: 035. Reverse Linked List](035-reverse-linked-list.md)
- [next: 038. Search a 2D Matrix II](038-search-a-2d-matrix-ii.md)
