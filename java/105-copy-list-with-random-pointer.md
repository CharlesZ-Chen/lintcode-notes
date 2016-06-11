[105. Copy List with Random Pointer](http://www.lintcode.com/problem/copy-list-with-random-pointer)

- [prev: 104. Merge k Sorted Lists](104-merge-k-sorted-lists.md)
- [next: 106. Convert Sorted List to Balanced BST](106-convert-sorted-list-to-balanced-bst.md)

---

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    /**
     * @param head: The head of linked list with a random pointer.
     * @return: A new head of a deep copy of the list.
     */
    public RandomListNode copyRandomList(RandomListNode head) {
        // write your code here
        // return hashMapWay(head);
        return nextPointerAsMapWay(head);
    }

    public RandomListNode nextPointerAsMapWay(RandomListNode head) {
        if (head == null) {
            return null;
        }

        RandomListNode curt, dummyClone, curtClone;

        // first deep copy next pointer
        curt = head;
        while(curt != null) {
            RandomListNode temp = curt.next;
            curt.next = new RandomListNode(curt.label);
            curt.next.next = temp;
            curt = temp;
        }

        // next deep copy random pointer
        curt = head;
        while (curt != null) {
            curt.next.random = curt.random == null ? null : curt.random.next;
            curt = curt.next.next;
        }

        dummyClone = new RandomListNode(0);

        // finally tear down two lists
        curt = head;
        curtClone = dummyClone;
        while (curt != null) {
            curtClone.next = curt.next;
            curt.next = curt.next.next;
            curtClone = curtClone.next;
            curt = curt.next;
        }

        return dummyClone.next;
    }

    public RandomListNode hashMapWay(RandomListNode head) {
        if (head == null) {
            return null;
        }

        HashMap<RandomListNode, RandomListNode> map = new HashMap<>();
        RandomListNode curt, dummyClone, prevClone, curtClone;

        // first loop deep copy next pointer
        curt = head;
        dummyClone = new RandomListNode(0);
        prevClone = dummyClone;
        while(curt != null) {
            prevClone.next = new RandomListNode(curt.label);
            map.put(curt, prevClone.next);
            curt = curt.next;
            prevClone = prevClone.next;
            
        }

        // second loop deep copy random pointer
        curt = head;
        curtClone = dummyClone.next;
        while (curt != null) {
            RandomListNode target = curt.random;
            curtClone.random = map.get(target);
            curt = curt.next;
            curtClone = curtClone.next;
        }

        return dummyClone.next;
    }
}
```

---

- [prev: 104. Merge k Sorted Lists](104-merge-k-sorted-lists.md)
- [next: 106. Convert Sorted List to Balanced BST](106-convert-sorted-list-to-balanced-bst.md)
