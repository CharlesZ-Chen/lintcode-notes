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

## quick sort version

Be award of **infinite recursion**! We have to have a **middle list** to refer the value equals to middle, and thus ensure that qsort(left) and qsort(right) would have a different mid value to partition the sub-list!

```java
    public ListNode sortList(ListNode head) {  
        if (head == null) {
            return null;
        }

        return qsort(head);
    }

    public ListNode qsort(ListNode head) {
        if (head == null) {
            return null;
        }
        if (head.next == null) {
            return head;
        }

        int mid = head.val;

        ListNode leftDummy = new ListNode(0);
        ListNode rightDummy = new ListNode(0);
        ListNode midDummy = new ListNode(0);
        ListNode left = leftDummy;
        ListNode right = rightDummy;
        ListNode middle = midDummy;

        while (head != null) {
            if (head.val < mid) {
                left.next = head;
                left = left.next;
            } else if (head.val > mid) {
                right.next = head;
                right = right.next;
            } else {
                middle.next = head;
                middle = middle.next;
            }
            head = head.next;
        }

        left.next = null;
        right.next = null;
        middle.next = null;

        left = qsort(leftDummy.next);
        right = qsort(rightDummy.next);

        return concat(left, midDummy.next, right);
    }

    public ListNode concat(ListNode left, ListNode middle, ListNode right) {
        ListNode dummy = new ListNode(0);
        ListNode tail = dummy;
        tail.next = left; tail = getTail(tail);
        tail.next = middle; tail = getTail(tail);
        tail.next = right;

        return dummy.next;
    }
    public ListNode getTail(ListNode head) {
        if (head == null) {
            return null;
        }

        while (head.next != null) {
            head = head.next;
        }
        return head;
    }
```

---

- [prev: 097. Maximum Depth of Binary Tree](097-maximum-depth-of-binary-tree.md)
- [next: 099. Reorder List](099-reorder-list.md)
