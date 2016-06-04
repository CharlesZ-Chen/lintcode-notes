[099. Reorder List](http://www.lintcode.com/problem/reorder-list)

- [prev: 098. Sort List](098-sort-list.md)
- [next: 100. Remove Duplicates from Sorted Array](100-remove-duplicates-from-sorted-array.md)

---

Just a Comble of findMiddle, reverseList, and mergeList;

**Note** the merge implementation in below algorithm is specific towards this problem, i.e. it just handle two cases:

- left and right list have same length.
- left has one more element than right.

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
     * @return: void
     */
    public void reorderList(ListNode head) {  
        if (head == null) {
            return;
        }
        ListNode mid, right, curt, next;

        // 1. find middle, get two list
        mid = getMiddle(head);

        // 2. reverse right part, cut to two lists
        // If list length is odd, then left.length = right.length + 1
        
        right = reverse(mid.next);
        mid.next = null;

        // 3. merge
        curt = head;
        next = right;
        // Promised by step 2 that we only need to handle below two situations
        // 1. left and right list have same length
        // 2. left has one more element than right
        while (curt != null) {
            ListNode temp = curt.next;
            curt.next = next;
            curt = next;
            next = temp;
        }
    }

    ListNode getMiddle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head.next;

        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }

    ListNode reverse(ListNode head) {
        ListNode prev = null;

        while (head != null) {
            ListNode temp = head.next;
            head.next = prev;
            prev = head;
            head = temp;
        }
        return prev;
    }
}

```

---

- [prev: 098. Sort List](098-sort-list.md)
- [next: 100. Remove Duplicates from Sorted Array](100-remove-duplicates-from-sorted-array.md)
