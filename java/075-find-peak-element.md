[075. Find Peak Element](http://www.lintcode.com/problem/find-peak-element)

- [prev: 074. First Bad Version](074-first-bad-version.md)
- [next: 076. Longest Increasing Subsequence](076-longest-increasing-subsequence.md)

---

Firgure out one thing: peak must exsits in a range that left is up, and right is down. Then we can binary search such a range to find peak.

```java
// keyword: binary search
// time complexity: O(log n)
// space complexity: O(1)
public class Solution {
    /** 
     *@param A : an integer rotated sorted array
     *@param target :  an integer to be searched
     *return : an integer
     */
    public int search(int[] A, int target) {
        if (A == null || A.length < 1) {
            return -1;
        }
        
        int start = 0, end = A.length - 1;
        
        while (start + 1 < end) {
            int mid = start + (end - start) / 2;

           if (A[mid] >= A[start]) { // first area
               if( target >= A[start] && target <= A[mid]) {
                   end = mid;
               } else {
                   start = mid;
               }
           }
           else { // secound area
               if (target >= A[mid] && target <= A[end]) {
                   start = mid;
               } else {
                   end = mid;
               }
           }
        }
        
        if(A[start] == target) {
            return start;
        }
        
        if(A[end] == target) {
            return end;
        }
        
        return -1;
    }
}

```

---

- [prev: 074. First Bad Version](074-first-bad-version.md)
- [next: 076. Longest Increasing Subsequence](076-longest-increasing-subsequence.md)
