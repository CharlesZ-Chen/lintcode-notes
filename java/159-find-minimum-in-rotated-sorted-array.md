[159. Find Minimum in Rotated Sorted Array](http://www.lintcode.com/problem/find-minimum-in-rotated-sorted-array)

- [prev: 158. Two Strings Are Anagrams](158-two-strings-are-anagrams.md)
- [next: 160. Find Minimum in Rotated Sorted Array II](160-find-minimum-in-rotated-sorted-array-ii.md)

---
Mine solution is quite a struggle... I've bited by a lot corner cases:

- corner case 1: [5,1,2,3,4]
- corner case 2: [1,2,3,4,5]
- corner case 3: [2,3,4,5,1]

[Jiuzhang solution](http://www.jiuzhang.com/solutions/find-minimum-in-rotated-sorted-array/) is quite smart, but I still not understand that how to transfer this problem to compare with the last element in a rotated array, so that it can ensure to find the min element in an elegant way...

```java
public class Solution {
    /**
     * @param num: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] num) {
        // write your code here
        if (num == null || num.length < 1) {
            return -1;
        }
        
        int start = 0;
        int end = num.length - 1;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int val = num[mid];
            
            if (val > num[0]) {
                start = mid + 1;
            } else {
                end = mid;
            }
        }
    
        if (end == num.length - 1) {
            return num[0] > num[end] ? num[end] : num[0];
        } else if ( num[start] < num[0]) {
            return num[start];
        } else{
            return num[end];
        }
    }
}
```
For convenience, I past the smiliar solution of Jiuzhang here:

```java
public class Solution {
    /**
     * @param num: a rotated sorted array
     * @return: the minimum number in the array
     */
    public int findMin(int[] num) {
        // write your code here
        if (num == null || num.length < 1) {
            return -1;
        }
        
        int start = 0;
        int end = num.length - 1;
        int target = num[num.length - 1];
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;
            int val = num[mid];
            
            if (val > target) {
                start = mid + 1;
            } else {
                end = mid;
            }
        }
        
        if (num[start] <= target) {
            return num[start];
        } else {
            return num[end];
        }
    }
}
```
---

- [prev: 158. Two Strings Are Anagrams](158-two-strings-are-anagrams.md)
- [next: 160. Find Minimum in Rotated Sorted Array II](160-find-minimum-in-rotated-sorted-array-ii.md)
