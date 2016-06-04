[104. Merge k Sorted Lists](http://www.lintcode.com/problem/merge-k-sorted-lists)

- [prev: 103. Linked List Cycle II](103-linked-list-cycle-ii.md)
- [next: 105. Copy List with Random Pointer](105-copy-list-with-random-pointer.md)

---

## PriorityQueue Solution

Building a min heap, each iteration add the current minValue Node to dummyList.

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
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        if (lists == null || lists.size() < 1) {
            return null;
        }

        PriorityQueue<ListNode> heap = new PriorityQueue<>(10, new ListCmp());
        ListNode dummy = new ListNode(0);
        ListNode curt = dummy;

        for (int i = 0; i < lists.size(); i++) {
            ListNode curtList = lists.get(i);
            if (curtList != null) {
                heap.offer(lists.get(i));
            }
        }

        while(heap.size() > 1) {
           ListNode minNode = heap.poll();
           if (minNode.next != null) {
               heap.offer(minNode.next);
           }
            // minNode.next = null;
            curt.next = minNode;
            curt = curt.next;
        }

        curt.next = heap.poll();

        return dummy.next;
    }

    class ListCmp implements Comparator<ListNode> {
        @Override
        public int compare(ListNode l1, ListNode l2) {
            return l1.val - l2.val;
        }
    }
}

```

## Divide and Conquer Top-down

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
     * @param lists: a list of ListNode
     * @return: The head of one sorted list.
     */
    public ListNode mergeKLists(List<ListNode> lists) {  
        if (lists == null || lists.size() < 1) {
            return null;
        }

        switch(lists.size()) {
            case 1: return lists.get(0);
            case 2: return mergeAsOneSortedList(lists.get(0), lists.get(1));
        }

        int mid = lists.size()/2;
        ListNode left = mergeKLists(lists.subList(0, mid));
        ListNode right = mergeKLists(lists.subList(mid, lists.size()));

        return mergeAsOneSortedList(left, right);
    }

    public ListNode mergeAsOneSortedList(ListNode fst, ListNode snd) {
        if (fst == null) {
            return snd;
        }

        if (snd == null) {
            return fst;
        }

        ListNode dummy = new ListNode(0);
        ListNode curt = dummy;

        while(fst != null && snd != null) {
            if (fst.val < snd.val) {
                curt.next = fst;
                fst = fst.next;
            } else {
                curt.next = snd;
                snd = snd.next;
            }
            curt = curt.next;
        }

        curt.next = fst == null ? snd : fst;

        return dummy.next;
    }
}

```

---

- [prev: 103. Linked List Cycle II](103-linked-list-cycle-ii.md)
- [next: 105. Copy List with Random Pointer](105-copy-list-with-random-pointer.md)
