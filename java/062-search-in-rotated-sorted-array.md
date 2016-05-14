[062. Search in Rotated Sorted Array](http://www.lintcode.com/problem/search-in-rotated-sorted-array)

- [prev: 061. Search for a Range](061-search-for-a-range.md)
- [next: 063. Search in Rotated Sorted Array II](063-search-in-rotated-sorted-array-ii.md)

---
Key point is to figure out how to use S,E,M to determine which area T belongs (left of M or right of M). We use two ascending lines to represents a RSA, then first determine which area M fall on, followed by determine whether T is on the left of M or on the right of M.

```java
// keyword: binary search, keep answer part
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

- [prev: 061. Search for a Range](061-search-for-a-range.md)
- [next: 063. Search in Rotated Sorted Array II](063-search-in-rotated-sorted-array-ii.md)
