[098. Sort List](http://www.lintcode.com/problem/sort-list)

- [prev: 097. Maximum Depth of Binary Tree](097-maximum-depth-of-binary-tree.md)
- [next: 099. Reorder List](099-reorder-list.md)

---

## Merge Sort Recursion Version

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
     * @return: You should return the head of the sorted linked list,
                    using constant space complexity.
     */
    public ListNode sortList(ListNode head) {  
        if (head == null) {
            return null;
        }

        return mergeSort(head);
    }

    public ListNode mergeSort(ListNode head) {
        if (head.next == null) {
            return head;
        }
        ListNode slow = head;
        ListNode fast = head.next.next;

        while (fast != null) {
            slow = slow.next;
            fast = fast.next;
            if (fast != null) {
                fast = fast.next;
            }
        }

        ListNode left = mergeSort(slow.next);
        slow.next = null;
        ListNode right = mergeSort(head);

        ListNode dummy = new ListNode(0);
        ListNode scanner = dummy;

        while (left != null || right != null) {
            if (left == null || right == null) {
                scanner.next = left == null ? right : left;
                break;
            }
            if (left.val < right.val) {
                scanner.next = left;
                left = left.next;
                scanner = scanner.next;
            } else {
                scanner.next = right;
                right = right.next;
                scanner = scanner.next;
            }
        }

        return dummy.next;
    }
}
```

---

- [prev: 097. Maximum Depth of Binary Tree](097-maximum-depth-of-binary-tree.md)
- [next: 099. Reorder List](099-reorder-list.md)
