[096. Partition List](http://www.lintcode.com/problem/partition-list)

- [prev: 095. Validate Binary Search Tree](095-validate-binary-search-tree.md)
- [next: 097. Maximum Depth of Binary Tree](097-maximum-depth-of-binary-tree.md)

---

#Double Dummy Node

Using leftDummy and rightDummy records less than x part and great or equal to x part. This trick makes life easier!

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
     * @param x: an integer
     * @return: a ListNode 
     */
    public ListNode partition(ListNode head, int x) {
        if (head == null) {
            return null;
        }

        ListNode leftDummy = new ListNode(0);
        ListNode rightDummy = new ListNode(0);
        leftDummy.next = head;
        rightDummy.next = head;

        ListNode left = leftDummy;
        ListNode right = rightDummy;

        while(head != null) {
            if (head.val < x) {
                left.next = head;
                left = head;
            } else {
                right.next = head;
                right = head;
            }
            head = head.next;
        }

        right.next = null;
        left.next = rightDummy.next;

        return leftDummy.next;
    }
    
}

```

---

- [prev: 095. Validate Binary Search Tree](095-validate-binary-search-tree.md)
- [next: 097. Maximum Depth of Binary Tree](097-maximum-depth-of-binary-tree.md)
